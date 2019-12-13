1. Na psaní složených závorek používáme [Allman](https://en.wikipedia.org/wiki/Indentation_style#Allman_style) styl. Každou závorku na samostatný řádek. Vyjímku povolujeme u vícenásobných `using` bloků.
2. Odsayujeme pomocí 4 mezer (nepoužíváme tab).
3. Používáme `camelCase` pro interní a privátní fieldy a kde je to možné, použijeme `readonly`. Pokud je field siatický, klíčové slovo `readonly` je po `static` (tzn. `static readonly` ne `readonly static`). Veřejné členy nepoužíváme, pokud to není nutné a píšeme je `PascalCasing` bez prefixů.
```
private ProjectDto project;
private ProjectApi projectApi;
private HtmlHelper htmlHelper;
```
4. Nepoužíváme `this.` pokud to není opravdu nutné.
5. Vždy uvádíme viditelnost (tzn. `private string _foo` ne `string _foo`). Viditelnost je vždy první (tzn. `public abstract` ne `abstract public`).
6. Import namespaců je na začátku **mimo** namespace deklaraci. Řadíme je abecedně (včetně systémových).
7. Nikdy nepouživáme více než jeden prázfný řádek za sebou.
8. Odstraňujeme zbytečné mezery na konci řádků. Např `if (someVar == 0)...`, kde tečky jsou zbytečné mezery.
9. Použiváme `var` když je zcela zřetelné o jaký typ se jedná (tzn. `var stream = new FileStream(...)` ne `var stream = OpenStandardInput()`).
10. Datové typy zapisujeme klíčovými slovy ne BCL typy (tzn. `int`, `string`, `float` místo `Int32`, `String`, `Single`, etc). To samé platí pro volání metod (tzn. `int.Parse` místo `Int32.Parse`).
11. Konstanty píšeme PascalCase (tzn. `public const string ShippingType` ne `public const string SHIPPING_TYPE`). Vyjímkou jsou *interop* (konstanty z Windows API). Ty zapisujeme stejně jak jsou ve Windows API.
12. Vždy když je to relevantní, píšeme `nameof(...)` místo `"..."`.
13. Délka jednoho řádku nepřesahne 150 znaků. (*Testovácí projekty mají vyjímku, neboť se vnich často použivají dlouhe názvy metod apod.* )
14. Při zalamování řádku, operátoru `.`, `=>`, `?:`, `&&` dáváme na začátek následujícího a ne na konec předešlého. (Vyjímka je pro operátor `=>` jestliže je použitý v parametru metody, která je lambda funkcí.).

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

15. Obecně se snažíme nepoužívat komentaře v našem běžném kódu. Pokud už takový komentář napíšu musí jasně říkat **proč** je tento řádek okomentován. (Dokumentační komentáře veřejných věcí používáme podle potřeby.)
16. Všechny `private` proměnné definujeme na začátku třídy. `Protected` a `public` se deklarují až po konstruktorech.

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
