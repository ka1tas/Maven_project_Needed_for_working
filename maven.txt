****************************************************************************POM.XML***********************************************************************************

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.sampoo</groupId>
	<artifactId>artifact</artifactId>
	<version>1</version>
	<packaging>war</packaging>

	<name>artifact</name>
	<description>Demo project for Spring Boot</description>
	
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.6.RELEASE</version>
		<relativePath /> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>



		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-jersey</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>5.1.47</version>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>
		
	<!-- <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency> -->
		
	<!-- 	<dependency>
			<groupId>io.jsonwebtoken</groupId>
			<artifactId>jjwt</artifactId>
			<version>0.6.0</version>
		</dependency>
		 -->
		
	<!-- 	<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-test</artifactId>
			<scope>test</scope>
		</dependency> -->
	
	
    

		
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-all</artifactId>
    <version>2.0.2-beta</version>
    <scope>test</scope>
</dependency>
		
		<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-dbcp2</artifactId>
    <version>2.1.1</version>
</dependency>
		

	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>


</project>



**********************************************************************************************************************************************************************


**************************************************************************/APPLICATION.PROPERTIES/********************************************************************


spring.datasource.url=jdbc:mysql://localhost:3306/artifact

spring.datasource.username=root
#spring.datasource.password=mysqlCT5
spring.datasource.password=root
spring.jpa.properties.hibernate.current_session_context_class=org.springframework.orm.hibernate5.SpringSessionContext
spring.datasource.driver.class=com.mysql.jdbc.Driver
spring.jackson.serialization.FAIL_ON_EMPTY_BEANS=false


# HikariCP settings
# spring.datasource.hikari.*
server.servlet.context-path=/artifact
spring.datasource.hikari.connection-timeout=60000
spring.datasource.hikari.maximum-pool-size=5
spring.jmx.enabled=false

# Jackson config
spring.jackson.serialization.fail-on-empty-beans=false



# logging
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} %M - %msg%n
logging.level.org.hibernate.SQL=debug
#logging.level.org.hibernate.type.descriptor.sql=trace
logging.level.=error
#logging.level.org.hibernate.type=trace

logging.level.com.sampoo.signup.=debug
logging.org.hibernate.type.descriptor.sql.BasicBinder=TRACE


**********************************************************************************************************************************************************************


************************************************************************APP.JAVA************************************************************************************

package com.sampoo.artifact;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.builder.SpringApplicationBuilder;
import org.springframework.boot.web.servlet.support.SpringBootServletInitializer;

@SpringBootApplication
public class App extends SpringBootServletInitializer {

	@Override
	protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
		return application.sources(App.class);
	}

	public static void main(String args[]) {
		SpringApplication.run(App.class, args);
	}

}

**********************************************************************************************************************************************************************

****************************************************************************/MockitoTest/*****************************************************************************

package com.sampoo.artifact.mockito;


import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.times;
import static org.mockito.Mockito.verify;
import static org.mockito.Mockito.when;

import org.junit.Before;
import org.junit.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.sampoo.artifact.bean.AuthenticationStatus;
import com.sampoo.artifact.bean.Language;
import com.sampoo.artifact.bean.Role;
import com.sampoo.artifact.bean.SignUpStatus;
import com.sampoo.artifact.bean.User;
import com.sampoo.artifact.dao.LanguageRepository;
import com.sampoo.artifact.dao.RoleRepository;
import com.sampoo.artifact.dao.UserRepository;
import com.sampoo.artifact.service.UserService;


public class UserSeviceMockito {
	
	private static final Logger LOGGER = LoggerFactory.getLogger(UserSeviceMockito.class);
	
	@Mock
	private UserRepository userRepository;
	
	@Mock
	private LanguageRepository languageRepository;
	
	@Mock
	private RoleRepository roleRepository;

	@InjectMocks
	private UserService service;

	@Before
	public void setUp() throws Exception {
		MockitoAnnotations.initMocks(this);
	}
	
	@Test
	public void testSuccesfullLogin() {
		LOGGER.info("START of testSuccesfullLogin() testing in UserSeviceMockito");
		User testUser = new User();
		testUser.setEmail("saikat@gmail.com");
		testUser.setPassword("12345");
		
		when(userRepository.findByEmail(testUser.getEmail())).thenReturn(testUser);

		AuthenticationStatus expectedstatus = new AuthenticationStatus();
		expectedstatus.setAuthStatus(true);
		expectedstatus.setUser(testUser);
		LOGGER.debug("status Should be test: "+ expectedstatus);
		AuthenticationStatus status = service.login(testUser);
		LOGGER.debug("status from test: "+ status);
		verify(userRepository, times(1)).findByEmail(testUser.getEmail());
		assertEquals(true, expectedstatus.equals(status));
		LOGGER.info("END of testSuccesfullLogin() testing in UserSeviceMockito");
	}
	
	@Test
	public void testFailedLogin() {
		LOGGER.info("START of testFailedLogin() testing in UserSeviceMockito");
		User testUser = new User();
		testUser.setEmail("saikat@gmail.com");
		testUser.setPassword("12345");
		
		when(userRepository.findByEmail(testUser.getEmail())).thenReturn(null);

		AuthenticationStatus expectedstatus = new AuthenticationStatus();
		expectedstatus.setAuthStatus(false);
		//expectedstatus.setUser(testUser);
		LOGGER.debug("status Should be test: "+ expectedstatus);
		AuthenticationStatus status = service.login(testUser);
		LOGGER.debug("status from test: "+ status);
		verify(userRepository, times(1)).findByEmail(testUser.getEmail());
		assertEquals(true, expectedstatus.equals(status));
		LOGGER.info("END of testFailedLogin() testing in UserSeviceMockito");
	}
	
	
	
	@Test
	public void testSuccesfullSignup() {
		LOGGER.info("START of testSuccesfullSignup() testing in UserSeviceMockito");
		
		Role testRole = new Role(1,"Admin");
		Language testLanguage = new Language(1, "en");
		User testUser = new User(0,"Saikat","saikat@gmail.com","123456","no",testRole,testLanguage);
		
		when(userRepository.findByEmail(testUser.getEmail())).thenReturn(null);
		when(roleRepository.findById(testUser.getRole().getId())).thenReturn(testRole);
		when(languageRepository.findById(testUser.getLanguage().getId())).thenReturn(testLanguage);
		when(userRepository.save(testUser)).thenReturn(testUser);

		SignUpStatus expectedstatus = new SignUpStatus();
		expectedstatus.setEmailExist(false);
		expectedstatus.setSignupStatus(true);
		
		
		LOGGER.debug("status Should be test: "+ expectedstatus);
		SignUpStatus status = service.save(testUser);
		LOGGER.debug("status from test: "+ status);
		verify(userRepository, times(1)).save(testUser);
		assertEquals(true, expectedstatus.equals(status));
		LOGGER.info("END of testSuccesfullSignup() testing in UserSeviceMockito");
	}
	
	
	
	@Test
	public void testExistingEmailWhileSignup() {
		LOGGER.info("START of testExistingEmailWhileSignup() testing in UserSeviceMockito");
		
		Role testRole = new Role(1,"Admin");
		Language testLanguage = new Language(1, "en");
		User testUser = new User(0,"Saikat","saikat@gmail.com","123456","no",testRole,testLanguage);
		
		when(userRepository.findByEmail(testUser.getEmail())).thenReturn(testUser);
		when(roleRepository.findById(testUser.getRole().getId())).thenReturn(testRole);
		when(languageRepository.findById(testUser.getLanguage().getId())).thenReturn(testLanguage);
		when(userRepository.save(testUser)).thenReturn(testUser);

		SignUpStatus expectedstatus = new SignUpStatus();
		expectedstatus.setEmailExist(true);
		expectedstatus.setSignupStatus(false);
		
		
		LOGGER.debug("status Should be test: "+ expectedstatus);
		SignUpStatus status = service.save(testUser);
		LOGGER.debug("status from test: "+ status);
		verify(userRepository, times(0)).save(testUser);
		assertEquals(true, expectedstatus.equals(status));
		LOGGER.info("END of testExistingEmailWhileSignup() testing in UserSeviceMockito");
	}
	
	
	

}


**********************************************************************************************************************************************************************

************************************************************************************/SpringBoot Test/****************************************************************


package com.sampoo.artifact.mockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.post;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import org.junit.Before;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.ExpectedException;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import org.springframework.web.context.WebApplicationContext;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SignupControllerMockMVC {
	private static final Logger LOGGER = LoggerFactory.getLogger(SignupControllerMockMVC.class);

	@Autowired
	private WebApplicationContext webApplicationContext;

	private MockMvc mockMvc;

	@Rule
	public ExpectedException exceptionRule = ExpectedException.none();

	@Before
	public void setup() {
		mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext).build();
	}

	@Test
	public void testSuccessfullSignup() throws Exception {
		LOGGER.info("START");
		String USER_DATA = "{\"email\" : \"sankar@sinha.com\"" + "," + "\"name\" : \"Sankar\"" + "," + "\"role\" : {\"id\":1}" + 
		"," + "\"language\" :{\"id\":1}" + "\"password\" : \"saikat12\" }";
		mockMvc.perform(post("/signup/add").content(USER_DATA).contentType("application/json;charset=UTF-8"))
				.andExpect(status().isOk()).andExpect(jsonPath("$.signupStatus").value("true"));

		LOGGER.info("END");
	}

	
	

}


********************************************************************************************************************************************************************


**************************************************************************/Excepction Controller/***************************************************************

package com.sampoo.artifact.rest;


import java.time.ZonedDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Set;

import javax.validation.ConstraintViolation;
import javax.validation.ConstraintViolationException;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;

import com.sampoo.artifact.bean.ErrorResponse;

public class ExceptionController {

	private static final Logger LOGGER = LoggerFactory.getLogger(ExceptionController.class);

	@ExceptionHandler(Exception.class)
	public ResponseEntity<ErrorResponse> handleError(Exception ex) {
		LOGGER.info("start");
		LOGGER.error(ex.getMessage(), ex);
		ErrorResponse error = new ErrorResponse();
		error.setTimestamp(ZonedDateTime.now().format(DateTimeFormatter.ISO_INSTANT));
		LOGGER.debug("error : {} ", error);
		ResponseEntity<ErrorResponse> response = null;
		if (ex instanceof ConstraintViolationException) {
			error.setReasonCode(HttpStatus.BAD_REQUEST.value());
			ConstraintViolationException constraintException = (ConstraintViolationException) ex;
			Set<ConstraintViolation<?>> set = constraintException.getConstraintViolations();
			String errorMessage = "Input Validation Failed:";
			for (ConstraintViolation<?> constraintViolation : set) {
				errorMessage += constraintViolation.getMessageTemplate() + ",";
			}
			errorMessage = errorMessage.substring(0, errorMessage.length() - 1);
			error.setErrorMessage(errorMessage);
			response = new ResponseEntity<ErrorResponse>(error, HttpStatus.BAD_REQUEST);
		} else {
			error.setReasonCode(HttpStatus.INTERNAL_SERVER_ERROR.value());
			error.setErrorMessage(ex.getMessage());
			response = new ResponseEntity<ErrorResponse>(error, HttpStatus.INTERNAL_SERVER_ERROR);
		}
		return response;
	}
}


**********************************************************************************************************************************************************************

*************************************************************************************ErrorResponse Bean **************************************************************

package com.sampoo.artifact.bean;

public class ErrorResponse {

	private static final long serialVersionUID = 5776681206288518465L;

	private String timestamp;
	private String errorMessage;
	private int reasonCode;

	public String getErrorMessage() {
		return errorMessage;
	}

	public void setErrorMessage(String errorMessage) {
		this.errorMessage = errorMessage;
	}

	public int getReasonCode() {
		return reasonCode;
	}

	public void setReasonCode(int reasonCode) {
		this.reasonCode = reasonCode;
	}

	public String getTimestamp() {
		return timestamp;
	}

	public void setTimestamp(String timestamp) {
		this.timestamp = timestamp;
	}

	public static long getSerialversionuid() {
		return serialVersionUID;
	}
}

*********************************************************************************************************************************************************************

