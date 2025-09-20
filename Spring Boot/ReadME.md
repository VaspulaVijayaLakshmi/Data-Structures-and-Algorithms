Spring Boot


@Configuration
@PropertySource("classpath:application.properties") // load the properties file
public class AppConfig {

    @Value("${db.driver}")
    private String driver;

    @Value("${db.url}")
    private String url;

    @Value("${db.username}")
    private String username;

    @Value("${db.password}")
    private String password;

    @Bean
    public DataSource dataSource() {
        BasicDataSource ds = new BasicDataSource();
        ds.setDriverClassName(driver);
        ds.setUrl(url);
        ds.setUsername(username);
        ds.setPassword(password);
        return ds;
    }
}
_________________________


Using @Value with a properties file

Create application.properties (in src/main/resources):

db.driver=com.mysql.cj.jdbc.Driver
db.url=jdbc:mysql://localhost:3306/testdb
db.username=root
db.password=password


_______________________



Spring 



<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans 
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/testdb"/>
        <property name="username" value="root"/>
        <property name="password" value="password"/>
    </bean>

</beans>


______________________________









