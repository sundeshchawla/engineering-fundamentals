Key things to absorb:

Complex object with many optional/required fields
Builder separates construction from representation
Director class (optional) — orchestrates the build steps
Method chaining is the C# idiom



eg.

ShopBuilder builder = new ShopBuilder();


builder
    .WithWalls(concrete)
    .WithGates(2)
    .Build();


method chaining, always returning "this".
finally when Build() is called then should return the object being built internally but not being returned
untill all operationsa re done.



When to use: 4+ constructor params, especially optional ones — telescoping constructor problem(aadhe null pass krre hote h, majoruity not needed in const,
then we create small constructors that ultimately call the larger one with passing null null)
C# alternative: object initializers work for simple cases, Builder wins when you need validation logic in Build()
Real Chase example: building an HttpClient request with headers, body, timeout, retry config


EXAMPLE

// Product
public class HttpRequest
{
    public string Url { get; set; }
    public string Method { get; set; }
    public Dictionary<string, string> Headers { get; set; } = new();
    public string Body { get; set; }
    public int TimeoutMs { get; set; }
}

// Builder
public class HttpRequestBuilder
{
    private readonly HttpRequest _request = new();

    public HttpRequestBuilder WithUrl(string url)
    {
        _request.Url = url;
        return this; // enables chaining
    }

    public HttpRequestBuilder WithMethod(string method)
    {
        _request.Method = method;
        return this;
    }

    public HttpRequestBuilder WithHeader(string key, string value)
    {
        _request.Headers[key] = value;
        return this;
    }

    public HttpRequestBuilder WithBody(string body)
    {
        _request.Body = body;
        return this;
    }

    public HttpRequestBuilder WithTimeout(int ms)
    {
        _request.TimeoutMs = ms;
        return this;
    }

    public HttpRequest Build() => _request;
}

// Usage — clean and readable
var request = new HttpRequestBuilder()
    .WithUrl("https://api.chase.com/bookings")
    .WithMethod("POST")
    .WithHeader("Authorization", "Bearer token123")
    .WithBody("{\"flightId\": 99}")
    .WithTimeout(5000)
    .Build();