Spring Provide Two Level of Exception Handling
1. Controller Level
		When service throws an error, that error we can catch in controller Class.
		@ExceptionHandler(NullPointerException.class) :when Null pointer Exception occurs 
		method will called which are annotated with it.
		
``` Java
public class ProductNotFoundException extends RuntimeException{  
  
    public ProductNotFoundException(){  
        super("Product Does Not Exists");  
    }  
    public ProductNotFoundException(String message){
	    super(message);
    }
}
```

``` Java
@Service  
public class FakeStoreProductService implements ProductServices{  
    RestTemplate restTemplate;  
    static  String URL = "https://fakestoreapi.com/products/";  
    @Autowired  
    public FakeStoreProductService(RestTemplate restTemplate){  
        this.restTemplate = restTemplate;  
    }
    @Override  
	public Product getSingleProduct(String id) {  
	    FakeStoreProductDTO productDTO =  restTemplate.getForObject(  
            URL + id,  
            FakeStoreProductDTO.class);  
		// Throw Exception
		if(productDTO == null) 
			throw new ProductNotFoundExecption();
	    return new Product(productDTO);  
	  }
  }


@RestController
public class ProductController {  
  
    ProductServices productService;  
    @Autowired  
    public ProductController( ProductServices productService){  
        this.productService = productService;  
    }  
    
    @GetMapping("/{id}")   
    public ResponseEntity<Product> getSingleProduct(@PathVariable("id") String id){  
        return new ResponseEntity<>(  
                productService.getSingleProduct(id),//Exception Line  
                HttpStatus.NOT_FOUND  
        );  
    }  
  //-----------Exception Handler Controller Level-----------------------------
    @ExceptionHandler(ProductNotFoundException.class)//Exception Catched Here  
    public ResponseEntity<String> productNotFound(ProductNotFoundException e){  
        return new ResponseEntity<>(e.getMessage(),HttpStatus.NOT_FOUND);  
    }  
}
```
This is Example Code, when service throws  ProductNotFoundException error that exception will handle by Controller's  <u>productNotFoundException</u> method.

2. GLOBAL LEVEL EXCEPTION HANDLING
		@ControllerAdvice is an annotation ,to handle Exception that not handle in Controllers 
``` Java
@ControllerAdvice  
public class ControllerAdvices {  
  
    @ExceptionHandler(ProductNotFoundException.class)  
    public ResponseEntity<String> productNotFound(ProductNotFoundException exception){  
        return new ResponseEntity<>(exception.getMessage(),  
                HttpStatus.NOT_FOUND);  
    }  
}
```