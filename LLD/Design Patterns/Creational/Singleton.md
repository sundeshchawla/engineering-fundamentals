Single instance

use cases like logger, db connector


rule of thumb:

keep constructor private
create static method that acts as constructor
    it gets the instance stored in a static field.

    if multi threaded env, first get lock, then check if instance null.



When to use: shared resource (DB connection pool, config, logger)
When NOT to use: makes unit testing hard (can't mock it easily) — flag this
C# tip: Lazy<T> handles thread-safety for you. Don't roll your own double-checked locking.

my example


public class Logger 
{
    private static Logger _logger;

    private Logger()
    {

    }

    public static GetInstance()
    {
        if(_logger == null)
        {
            getlock(){

                if(_logger == null)
                {
                    _logger = new Logger();
                }
            }
        }

        return _logger;
    }
    
}



thiis is claudes suggested code

// Thread-safe Singleton using Lazy<T> — preferred in C#
public sealed class ConfigurationManager
{
    private static readonly Lazy<ConfigurationManager> _instance =
        new Lazy<ConfigurationManager>(() => new ConfigurationManager());

    public static ConfigurationManager Instance => _instance.Value;

    private ConfigurationManager() { }

    public string GetSetting(string key) => $"value_for_{key}";
}

// Usage
var config = ConfigurationManager.Instance;