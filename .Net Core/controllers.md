# Controllers

Controllers in ASP.Net Core inherit from the Controller class. For API controllers, you can use the controller base class, which is a stripped-down version without the view and razor features you only need in a web app.

```csharp
namespace LandonApi.Controllers
{
   // route attributes to tell the routing system which routes they should handle.
    [Route("/")]
    //  tell the routing system which routes they should handle.
    [ApiController]
    public class RootController : ControllerBase
    {
   //This explicitly tells ASP.Net Core that it should handle the Get verb
        [HttpGet(Name = nameof(GetRoot))]
// Returning iActionResult gives us the flexibility to return http status codes or JSON responses.
        public IActionResult GetRoot()
        {
            var response = new
            {
                href = Url.Link(nameof(GetRoot), null)
            };

            return Ok(response);
        }
    }
}
```