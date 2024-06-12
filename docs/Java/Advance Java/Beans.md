Beans is Global Object which store in application context, that allow to use that single object anywhere in application.


Example
Here we have two created beans, one of `RestTemplate`,one of `Webclient`.
Spring will can this method and store return object in application context.
This object stored in application context are beans, which we can use in any class through dependency inversion(@AutoWired annotation in constructor of class) .


```Java
@Configuration  
public class Beans {  
	// Get From application.properties files
	@Value("${application.FakeStoreURL}")    
    public static String URL;  
    @Bean  
    public RestTemplate getRestTemplate(){  
        return new RestTemplate();  
    }  
    
    @Bean  
    public WebClient webclient(){  
        return WebClient.builder().baseUrl(URL).
        defaultHeader(HttpHeaders.CONTENT_TYPE, MediaType.APPLICATION_JSON_VALUE)  
                .defaultUriVariables(Collections.singletonMap("url",URL)).build();  
    }  
}
```

# Using Beans

To Access beans,
1. Mark your class with any spring marker @Service| @Controller | @ControllerAdvicer|@RestController .......
2. Dependency injection, inject object through constructor parameter. 

``` Java
@Service("RestTemplateService")
public class MyService{
	RestTemplate restTemplate;
	@AutoWired
	MyService(RestTemplate restTemplate){
		this.restTemplate = restTemplate;
	}
} 
//                                     OR
@Controller
public class rootController{
	WebClient webClient;
	@AutoWired
	rootController(WebClient webClient){
		this.webClient = webClient;
	}
}

```

### @Qualifier
**Scenario:**

Imagine you have two implementations of the same interface, `UserService`:

- `UserServiceImpl1`
- `UserServiceImpl2`

Both are registered as Spring beans, but you only want to inject `UserServiceImpl1` into a specific component.

Method 1: is to annotate UserServiceImpl1 @primary but in big project this become finding needles in haystacks.

Method 2: is Use @qualifier at the time of dependency injection to specify which beans to inject.

for that you have to give name from components.
```Java
@Service("impl1")
class UserServiceImpl1{
	// code
}
```

Use @Qualifier to specify beans

```Java
@Controller
class UserController{
	UserService userService;
	UserController(@Qualifier("impl1") UserService userService){
		@Autowired
		this.userService = userService;
	}
}
```


