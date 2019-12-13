1. We use [Allman](https://en.wikipedia.org/wiki/Indentation_style#Allman_style) style braces, where each brace begins on a new line. One exception is that a `using` statement is permitted to be nested within another `using` statement by starting on the following line at the same indentation level, even if the nested `using` contains a controlled block.
2. We use four spaces of indentation (no tabs).
3. We use `camelCase` for internal and private fields and use `readonly` where possible. When used on static fields, `readonly` should come after `static` (e.g. `static readonly` not `readonly static`). Public fields should be used sparingly and should use `PascalCasing` with no prefix when used.
```
ProjectDto project;
ProjectApi projectApi;
HtmlHelper htmlHelper;
```
4. We avoid `this.` unless absolutely necessary.
5. We always specify the visibility, even if it's the default (e.g. `private string _foo` not `string _foo`). Visibility should be the first modifier (e.g. `public abstract` not `abstract public`).
6. Namespace imports should be specified at the top of the file, **outside** of namespace declarations, and should be sorted alphabetically (all of them).
7. Avoid more than one empty line at any time. For example, do not have two blank lines between members of a type.
8. Avoid spurious free spaces. For example avoid `if (someVar == 0)...`, where the dots mark the spurious free spaces.
9. We only use `var` when it's obvious what the variable type is (e.g. `var stream = new FileStream(...)` not `var stream = OpenStandardInput()`).
10. We use language keywords instead of BCL types (e.g. `int`, `string`, `float` instead of `Int32`, `String`, `Single`, etc) for both type references as well as method calls (e.g. `int.Parse` instead of `Int32.Parse`)
11. We use PascalCasing to name all our constant local variables and fields (e.g. `public const string ShippingType` instead of `public const string SHIPPING_TYPE`). The only exception is for interop (Windows API constants) code where the constant value should exactly match the name and value of the code you are calling via interop.
12. We use `nameof(...)` instead of `"..."` whenever possible and relevant.
13. Line of code should not exceed 150 characters. (*Test projects have exception because they use long method names and so on.* )
14. When we need to wrap a line, operators like `.`, `=>`, `?:`, `&&` are at the start of another line. (Operator `=>` have exception when  it is used as a lambda function.)

```
public class LineBreaks
{
    public LineBreaks() : base()
    {
    }

    public LineBreaks(string parameter1, string parameter2, string parameter3)
        : base(parameter1, parameter2, parameter3)
    {
    }

    private override void FooShort() => base.FooShort();

    private override void FooWithNameTooLongForOneLine()
        => base.FooWithNameTooLongForOneLine();

    private void LambdaAsMethodArgument(IWebHostBuilder builder) {
        builder.ConfigureServices(services =>
        {
            services.AddSingleton<IEmailSender, SmtpEmailSender>();
            services.AddTransient<ILogger>(serviceProvider => new Logger());
        });
    }
    
    private void Bar()
    {
        services.AddIdentityServer()
            .AddDeveloperSigningCredential()
            .AddInMemoryPersistedGrants()
            .AddInMemoryClients(clients.Value);
    }

    private void TernaryOperator(int count, string primaryKeyName)
    {
        int total = count > 0 ? count * _itemPrice : 0;

        IndexSchema primaryKey = string.IsNullOrWhiteSpace(primaryKeyName)
            ? null
            : new IndexSchema(primaryKeyName, IndexType.PrimaryKey);
    }
}
```

15. We generally avoid to use single line comments. When we write them it is important that comment tell us **why** this line of code is commented. (We use documentary comments as needed.)
16. We declare all `private` variables at the top of a class. `Protected` and `public` variables declare after constructor.

```
public class Account
{
  private readonly AccountRepository accountRepository;

  public Account(AccountRepository accountRepository)
  {
    // ...
  }

  public static string BankName;
  public DateTime DateClosed { get; set; }
  public decimal Balance { get; set; }   
}
```
