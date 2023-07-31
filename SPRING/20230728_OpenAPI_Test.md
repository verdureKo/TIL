# JSP 공공 포털 API 연동 구현 예제 실습

  1) 계정명 = jsp_openapi

  2) 계정 비밀번호 =  jsp_openapi


* DB 테이블명과 칼럼명으로 테이블을 생성합니다.

   1) 테이블명 = jsp_address

   2) 시퀀스명 = idx_seq

   3) 칼럼명(등록 번호) = address_id

   4) 칼럼명(기본 주소) = basic_address

   5) 칼럼명(상세 주소) = detail_address

```sql
SQL>create user jsp_openapi identified by jsp_openapi;

SQL>grant connect, resource, dba to jsp_openapi;

SQL>conn jsp_openapi/jsp_openapi;

SQL>show user

SQL>create table jsp_address(
    address_id number primary key,
    basic_address varchar2(80) not null,
    detail_address varchar2(50) not null
);

SQL> commit;

SQL> desc jsp_address;

SQL>create sequence idx_seq start with 0 minvalue 0;

SQL>select * from user_sequences;
-- 휴지통 내용(삭제 내용) 지울때 활용함

SQL>purge recyclebin;  
```

```java
package address.model;

public class Address {
	
	private int address_id;
	private String basic_address;
	private String detail_address;
	
	
	public Address(int address_id, String basic_address, String detail_address) {
		this.address_id = address_id;
		this.basic_address = basic_address;
		this.detail_address = detail_address;
	}
	
	public int getAddress_id() {
		return address_id;
	}
	public void setAddress_id(int address_id) {
		this.address_id = address_id;
	}
	public String getBasic_address() {
		return basic_address;
	}
	public void setBasic_address(String basic_address) {
		this.basic_address = basic_address;
	}
	public String getDetail_address() {
		return detail_address;
	}
	public void setDetail_address(String detail_address) {
		this.detail_address = detail_address;
	}
}
```

```java
package address.dao;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class AddressDAO {

	// 기본주소, 상세주소 등록
	public void insertAddress(Connection conn, String basic, String detail) 
			throws SQLException {
		System.out.println("AddressDAO.insertAddress()");
		try(PreparedStatement pstmt = conn.prepareStatement(
				"insert into jsp_address values(idx_seq.nextval,?,?)")) {
			pstmt.setString(1, basic);
			pstmt.setString(2, detail);
			
			pstmt.executeUpdate();
		}
	}
}
```

```java
package address.service;

import java.sql.Connection;
import java.sql.SQLException;

import address.dao.AddressDAO;
import jdbc.JdbcUtil;
import jdbc.connection.ConnectionProvider;
//주소 입력 기능을 제공하는 AddressService 클래스의 코딩 구현
public class AddressService {
	private AddressDAO addressDAO = new AddressDAO();
	
	public void insert(String basic, String detail) {
		Connection conn =null;
		try {
			conn = ConnectionProvider.getConnection();
			conn.setAutoCommit(false);
			// 주소 데이터 테이블에 삽입
			addressDAO.insertAddress(conn, basic, detail);	
			//성공시 커밋
			conn.commit();
		} catch (SQLException e) {
			JdbcUtil.rollback(conn);
			
		} catch (RuntimeException e) {
			JdbcUtil.rollback(conn);
			throw e;
		} finally {
			JdbcUtil.close(conn);
		}
	}
}
```

``java
package address.service;
//AddressService 클래스는 조회할 데이터가 존재하지 않으면
//익셉션을 발생시킨다. 먼저, address 테이블에 데이터가 존재하지 않을 때
//발생할 익셉션인 AddressInsertFailException 예외 처리를 구현한다.
public class AddressInsertFailException extends Exception {

}   
```

```java
package address.command;

import java.io.IOException;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import address.service.AddressService;
import mvc.command.CommandHandler;
//주소 등록을 처리할 AddressHandler를 구현하려고 한다.
//게시글 작성 폼을 보여주고 폼 전송을 처리하므로,
//GET 방식 요청과 POST 방식 요청을 별도의 메서드에서 처리한다.
//GET 방식 : 수정할 게시글 데이터를 읽어와 폼에 보여준다.
//POST 방식 : 전송한 요청 파라미터를 이용해서 게시글을 수정한다.
public class AddressHandler implements CommandHandler{
	
	private static final String FORM_VIEW = "/WEB-INF/view/addressForm.jsp";
	
	// 주소입력 기능을 제공하는 addressService 생성
	AddressService addressService = new AddressService();

	@Override
	public String process(HttpServletRequest req, HttpServletResponse res) 
			throws Exception {
		// equalsIgnoreCase : 같은 값 확인할 때, 대소문자 구분을 하지 않는다.
		// equals : 같은 값 확인할 때, 대소문자 구분을 한다.
		if(req.getMethod().equalsIgnoreCase("GET")) {
			return processForm(req,res);
		} else if (req.getMethod().equalsIgnoreCase("POST")) {
			return processSubmit(req, res);
		} else {
	        // 405 응답 코드 전송 (허용되지 않는 메소드 응답)
			res.setStatus(HttpServletResponse.SC_METHOD_NOT_ALLOWED);
			return null;
		}
	}

	// 폼 요청을 처리함
	private String processForm(HttpServletRequest req, HttpServletResponse res) 
			throws IOException {
		// 폼을 위한 뷰를 리턴한다.
		return FORM_VIEW;
	}

	// 폼 전송 처리한다.
	private String processSubmit(HttpServletRequest request, 
			HttpServletResponse response) {
		String basic_address = request.getParameter("basic_address");
		String detail_address = request.getParameter("detail_address");
		
		// 에러 정보를 담을 맵 객체를 생성하고, "errors" 속성에 저장
		Map<String, Boolean> errors = new HashMap<>();
		// 주소가 유효한지 검사한다.
		request.setAttribute("errors", errors);

		// 기본 주소가 빈칸 일 경우 에러발생 
		if(basic_address == null || basic_address.isEmpty()) {
			errors.put("basic_address", Boolean.TRUE);
		}
		// 상세 주소가 빈칸 일 경우 에러발생 
		if(detail_address == null || detail_address.isEmpty()) {
			errors.put("detail_address", Boolean.TRUE);
		}
	
		// 에러가 존재하면 FORM_VIEW 폼을 다시 보여준다.
		if(!errors.isEmpty()) {
			return FORM_VIEW;
		}
		
		try {
			// 주소입력 메서드 실행
			addressService.insert(basic_address, detail_address);
			return "/WEB-INF/view/addressSuccess.jsp";
			// Exception 예외가 발생하면 익셉션을 처리한다.
		} catch (Exception e) {
			// 404 응답 코드 전송(요청한 자원이 존재하지 않음)
			errors.put("AddressFail", Boolean.TRUE);
			return FORM_VIEW;
		}
	}
}
```

```java
package address.command;

import java.io.IOException;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import address.service.AddressService;
import mvc.command.CommandHandler;
//주소 검색을 처리할 SearchAddressHandler를 구현하려고 한다.
public class SearchAddressHandler implements CommandHandler{
	
	private static final String FORM_VIEW =
			"/WEB-INF/view/addressAPIPopup.jsp";
	
	// 주소입력 기능을 제공하는 addressService 생성
	AddressService addressService = new AddressService();

	@Override
	public String process(HttpServletRequest req, HttpServletResponse res) throws Exception {
		// equalsIgnoreCase : 같은 값 확인할 때, 대소문자 구분을 하지 않는다.
		// equals : 같은 값 확인할 때, 대소문자 구분을 한다.
		if(req.getMethod().equalsIgnoreCase("GET")) {
			return processForm(req,res);
		} else if (req.getMethod().equalsIgnoreCase("POST")) {
			return processSubmit(req, res);
		} else {
			// 405 응답 코드 전송 (허용되지 않는 메소드 응답)
			res.setStatus(HttpServletResponse.SC_METHOD_NOT_ALLOWED);
			return null;
		}
	}

	// 폼 요청을 처리함
	private String processForm(HttpServletRequest req, HttpServletResponse res) throws IOException {
		System.out.println("SearchAddressHandler.processForm()");
		// 폼을 위한 뷰를 리턴한다.
		return FORM_VIEW;
	}
	
	// 폼 전송 처리한다.
	private String processSubmit(HttpServletRequest request, HttpServletResponse response) {
		System.out.println("SearchAddressHandler.processSubmit()");
		// addressForm.jsp 에서 form 태그로 넘어온 파라미터값을 변수에 저장한다.
		String basic_address = request.getParameter("basic_address");
		String detail_address = request.getParameter("detail_address");
		
		System.out.println("기본주소 : "+basic_address);
		System.out.println("상세주소 : "+detail_address);
		
		// 에러 정보를 담을 맵 객체를 생성하고, "errors" 속성에 저장
		Map<String, Boolean> errors = new HashMap<>();
		// 주소가 유효한지 검사한다.
		request.setAttribute("errors", errors);
		
		// 기본 주소가 빈칸 일 경우 에러발생 
		if(basic_address == null || basic_address.isEmpty()) {
			errors.put("basic_address", Boolean.TRUE);
		}
		// 상세 주소가 빈칸 일 경우 에러발생 
		if(detail_address == null || detail_address.isEmpty()) {
			errors.put("detail_address", Boolean.TRUE);
		}
		
		// 에러가 존재하면 FORM_VIEW 폼을 다시 보여준다.
		if(!errors.isEmpty()) {
			return FORM_VIEW;
		}
		try {
			// 주소입력 메서드 실행
			addressService.insert(basic_address, detail_address);
			return "/WEB-INF/view/addressSuccess.jsp";
			// Exception 예외가 발생하면 익셉션을 처리한다.
		} catch (Exception e) {
			errors.put("AddressFail", Boolean.TRUE);
			// 404 응답 코드 전송(요청한 자원이 존재하지 않음)
			return FORM_VIEW;
		}
	}
}
```

run on server!

## JSP 및 프론트 앤드 개발

1. WebContent 폴더 안에 배포한 static 폴더(style.css, jquery-3.5.1.min.js) 파일을 넣어주기
2. WEB-INF 폴더 안에 view 폴더 생성 후 그 안에 addressForm.jsp 소스 코딩

```html
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>주소 등록</title>
<script>
<%-- 주소검색 팝업 호출 --%>
function fn_openAddressPopup(){
	var url = "searchAddress.do";
	var name = "AddressPopup";
	var option = "width=600, height=300, top=100, left=200, location=no"
	window.open(url, name, option);
}
<%-- 주소검색 팝업 호출 CallBack --%>
function callback_openAddressPopup(aParam){
	document.getElementById("basic_address").value = aParam["roadAddr"];
}
</script>
</head>
<body>
<h4>[주소 등록]</h4>
<form action="insert.do" method="POST">
	기본 주소:<br>
	<input style="width:40%" type="text" id="basic_address" name="basic_address" class="form-control" 
	onkeypress="javascript:enterSearch();" />
	<input type="button" onclick="javascript:fn_openAddressPopup();" value="검색"/>
	<br><br>
	상세 주소:<br>
	<input style="width:40%" name ="detail_address" type="text"/><br><br>
	<input type="submit" value="주소 등록">
	<a href="/JSP_OracleDB_OPENAPI"><input type="button" value="취소"></a>
</form>
</body>
</html>
```

```
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<script type="text/javascript" src="static/js/jquery-3.5.1.min.js"></script>
<link rel="stylesheet" href="static/css/style.css">
		
<script>
	<%-- 주소명으로 검색 --%>
	function getAddr(){
		
		$.ajax({
			 url :"http://www.juso.go.kr/addrlink/addrLinkApiJsonp.do" //인터넷망
			,type:"post"
			,data:$("#searchForm").serialize()
			,dataType:"jsonp"
			,crossDomain:true
			,success:function(jsonStr){
				var errCode = jsonStr.results.common.errorCode;
				var errDesc = jsonStr.results.common.errorMessage;
				if(errCode != "0"){
					alert(errCode+"="+errDesc);
				}else{
					if(jsonStr != null){
						makeListJson(jsonStr);
					}
				}
			}
		    ,error: function(xhr,status, error){
		    	alert("에러발생");
		    }
		});
	}
	
	<%-- 결과 테이블 생성 --%>
	function makeListJson(jsonStr){
		var htmlStr = "";
		$(jsonStr.results.juso).each(function(){
			htmlStr += "<tr onclick=\"javascript:chooseAddress('"+this.roadAddr+"', '"+this.jibunAddr+"', '"+this.zipNo+"');\">";
			htmlStr += "<td>";
			htmlStr += "<dl>"+this.roadAddr+"</dl>";
			htmlStr += "<dl>"+this.jibunAddr+"</dl>";
			htmlStr += "</td>";
			htmlStr += "<td>"+this.zipNo+"</td>";
			htmlStr += "</tr>";
		});
		$("#addressTableTbody").html(htmlStr);
	}
	
	<%-- Enter 키 이벤트 --%>
	function enterSearch() {
		var evt_code = (window.netscape) ? ev.which : event.keyCode;
		if (evt_code == 13) {    
			event.keyCode = 0;  
			fn_search();
		} 
	}
	
	<%-- 주소 선택 --%>
	function chooseAddress(roadAddr, jibunAddr, zipNo){
		var aParam = [];
		aParam["roadAddr"] = roadAddr;
		aParam["jibunAddr"] = jibunAddr;
		aParam["zipNo"] = zipNo;

		opener.callback_openAddressPopup(aParam);
		window.close();
	}
</script>
<title>apiSampleJSON jsp 소스 참고 코딩</title>
</head>
<body>
<form name="searchForm" id="searchForm" method="post" 
			  class="navbar-form navbar-left" 
			  role="search" onsubmit="event.preventDefault();">
				<input type="hidden" name="currentPage" value="1"/> <!-- 요청 변수 설정 (현재 페이지. currentPage : n > 0) -->
				<input type="hidden" name="countPerPage" value="100"/> <!-- 요청 변수 설정 (페이지당 출력 개수. countPerPage 범위 : 0 < n <= 100) -->
				<input type="hidden" name="resultType" value="json"/> <!-- 요청 변수 설정 (검색결과형식 설정, json) --> 
				<input type="hidden" id="confmKey" name="confmKey" value="이자리에 도로명주소API 승인키를 기재해 주시기 바랍니다"/> <!-- 요청 변수 설정 (승인키) -->
				<input style="width:50%" type="text" id="keyword" name="keyword"  placeholder="도로명+건물번호, 건물명, 지번을 입력하세요." onkeypress="javascript:enterSearch();" /><!-- 요청 변수 설정 (키워드) -->
				<input type="button"  onclick="getAddr();" value="검색"/>
		</form>
	<div>
		<table style="border:1px solid black; width:100%;">
			<thead>
				<tr>
					<th style="width:85%">주소</th>
					<th style="width:15%">우편번호</th>
				</tr>
			</thead>
			<tbody id="addressTableTbody">
			</tbody>
		</table>	
	</div>
</body>
</html>
```

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>주소 입력 성공</title>
</head>
<body>
<h4>* 주소 정보가 제대로 등록 처리 되었습니다.</h4>
<a href="/"><input type="button" value="처음으로"></a>
</body>
</html>
```

5. Run On Server

6. http://localhost:9003/

  [처음화면]
  "주소 등록" 버튼 클릭
       ↓
  [주소 등록]
  기본 주소: 에서 "검색" 버튼 클릭 - 기본 주소 선택
   - 상세 주소 입력 후 "주소 등록" 버튼 클릭

7. OracleDB에 생성된 테이블과 게시글 등록된 데이터를 확인

SQL> select * from tab;

SQL> select * from jsp_address;
