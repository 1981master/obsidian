```javascript
@RestController
@RequestMapping("/api/demo")
public class DemoController {

    @PostMapping("/user/{id}")
    public String handleAll(
            @PathVariable("id") String userId,                    // path variable
            @RequestParam(name = "type", required = false) String type,  // query param
            @RequestHeader(name = "X-Auth-Token", required = false) String token, // header
            @RequestBody(required = false) String body           // raw body as string
    ) {
        // Just for demonstration, return all values in one string
        return "PathVariable (id): " + userId +
               ", QueryParam (type): " + type +
               ", Header (X-Auth-Token): " + token +
               ", Body: " + body;
    }
}

```