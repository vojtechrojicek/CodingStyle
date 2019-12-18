Diky vsem co poslali svuj nazor.  
* Co nejdrive se pokusim prepsat tyto body a umistit vysledek nekam kam k tomu mame pristup.
* Mimo to vytvorim soubor `.editorconfig`, ktery by nam mel vetsinu techto bodu pomoci hlidat ve VS.   
* Do noveho projektu Itixis ho pridame a budeme snim pracovat. V kazdem pripadnem novem projektu bude taky.
* Do starych projektu (Herkules, LTD) ho davat nebudeme nebot bychom se z message/warningu zblaznili. 
* Nicmene piste podle techto bodu nove veci, pripadne pokud se budou upravovat stare tak postupne (s rozumem) refaktorovat.

## Vysledky dotazniku:

1. ![#32CD32](https://placehold.it/15/32CD32/000000?text=+) `100%` - Na psaní složených závorek používáme [Allman](https://en.wikipedia.org/wiki/Indentation_style#Allman_style) styl. Každou závorku na samostatný řádek. Vyjímku povolujeme u vícenásobných `using` bloků.  

2. ![#FFFF00](https://placehold.it/15/FFFF00/000000?text=+) `60%` - Odsazujeme pomocí 4 mezer (nepoužíváme tab).

> #### Reakce 1:
> *Ve VS Používám Tab, který automaticky nahrazuje 4 mezery. Je to trochu zavádějící.*
> #### Odpoved:
> Ano! Tak je to mysleno. Neni to mysleno, ze bychom meli psat 4* mezernik, ale at mame vsichni nastavene VisualStudio (nebo jakekoliv IDE, ktere kdo pouziva - mluvim o VisualStudioCode apod.) at si nastavi aby Tab psal 4 mezery (ne 3, ne 5).  
> **Jedna se o vychozi nastaveni, takze na 95% nemusi nikdo nic nastavovat.**

> #### Reakce 2:
> *Rozhodně ne. Používat tabulátor.*
> #### Odpoved:
> Doufam ze odpoved na otazku 1 to vysvetluje lepe :)

3.  ![#32CD32](https://placehold.it/15/32CD32/000000?text=+) `90%` - Používáme `camelCase` pro interní a privátní fieldy a kde je to možné, použijeme `readonly`. Pokud je field siatický, klíčové slovo `readonly` je po `static` (tzn. `static readonly` ne `readonly static`). Veřejné členy nepoužíváme, pokud to není nutné a píšeme je `PascalCasing` bez prefixů.
```
private ProjectDto project;
private ProjectApi projectApi;
private HtmlHelper htmlHelper;
```
> #### Reakce 1:
> *Co znamená "veřejné členy nepoužíváme"? Zahrnuje to i property?*
> #### Odpoved:
> Mozna jen chybny preklad z anglicke vety: *Public fields should be used sparingly and should use `PascalCasing` with no prefix when used.*  
> Chapu a myslim to tak, ze public property piseme `PascalCasing`, ale, ze primarne se snazime pouzivat jinou nez `public` viditelnost.
> #### Zaver:
> Doplnim priklad ze nepouzivame podtrzitka (ne `_camelCase`).

4. ![#FFFF00](https://placehold.it/15/FFFF00/000000?text=+) `75%` - Nepoužíváme `this.` pokud to není opravdu nutné.

> #### Reakce 1:
> *Nesouhlasím. Raději použít this než vytvářet patvary názvů fieldu/properties, abychom se vyhnuli použití stejného názvu jako v parametru konstruktoru.*
> #### Odpoved:
> Ano, to je v poradku. V bodu 3 jsme se shodli na pouzivani `camelCase` pro interní a privátní fieldy a je jasne, ze **nebudeme vymyslet jine nazvy fieldu** abychom se vyhli `this`, coz by zmensilo citatelnost. Pouziti `this.username = username;` v konstruktoru je naprosto OK. Tady je slovicko `this` vyznamove a je ho nutne pouzit.  
> Mysleno tak, aby se zbytecne neobjevovalo slovicko `this` kdyz nema zadny vyznam napr. : `this.Username = username;` ( Spravne: `Username = username;` ).  


5. ![#32CD32](https://placehold.it/15/32CD32/000000?text=+) `100%` - Vždy uvádíme viditelnost (tzn. `private string _foo` ne `string _foo`). Viditelnost je vždy první (tzn. `public abstract` ne `abstract public`).
6. ![#32CD32](https://placehold.it/15/32CD32/000000?text=+) `100%` - Import namespaců je na začátku **mimo** namespace deklaraci. Řadíme je abecedně (včetně systémových).
7. ![#32CD32](https://placehold.it/15/32CD32/000000?text=+) `100%` - Nikdy nepouživáme více než jeden prázfný řádek za sebou.
8. ![#32CD32](https://placehold.it/15/32CD32/000000?text=+) `100%` - Odstraňujeme zbytečné mezery na konci řádků. Např `if (someVar == 0)...`, kde tečky jsou zbytečné mezery.
9. ![#FFFF00](https://placehold.it/15/FFFF00/000000?text=+) `60%` - Použiváme `var` když je zcela zřetelné o jaký typ se jedná (tzn. `var stream = new FileStream(...)` ne `var stream = OpenStandardInput()`).

> #### Reakce:
> * *Nesouhlasím. Za mě je var v pohodě i ve druhé ze zmíněných situací. Stojím si za tím, že s použitím varu je kód přehlednější i v situacích, kdy není typ zřejmý.*  
> * *používal bych var úplně všude, pokud nepotřebuji explicitně přetypovat (např na interface)*  
> * *Jsem pro pouzivani var u dlouhych nazvu typu ci linq dotazu. Primitivni typy (int, string atd) uvadet explicitne.*
> #### Odpoved:
> Za me u typu jako `Dictionary<string, MojeKrasnaTrida<Generik1, Generik2>>` kazdy pochopi pouziti `var`.
> #### Zaver:
> Tento bod nechavame.

10. ![#32CD32](https://placehold.it/15/32CD32/000000?text=+) `100%` - Datové typy zapisujeme klíčovými slovy ne BCL typy (tzn. `int`, `string`, `float` místo `Int32`, `String`, `Single`, etc). To samé platí pro volání metod (tzn. `int.Parse` místo `Int32.Parse`).
11. ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) `50%` - Konstanty píšeme PascalCase (tzn. `public const string ShippingType` ne `public const string SHIPPING_TYPE`). Vyjímkou jsou *interop* (konstanty z Windows API). Ty zapisujeme stejně jak jsou ve Windows API.

> #### Reakce:
> * *Z hlediska svého osobního zvyku bych zanechal SHIPPING_TYPE. Ale nebazíruji na tom.*  
> * *Verze názvu s podtržítky se mi zdá přehlednější, ale na toto téma jsme již kdysi debatovali a byl jsem přehlasován :-)*  
> * *Nesouhlasím. Konstanty bych psal zásadně uppercase s podržítky. Za mě je podstatné, aby byly konstanty v kódu na první pohled rozeznatelné a tohle je za mě nejlepší způsob.*  
> * *Jsem pro UpperCase.*
> #### Odpoved:
> Kontroverzni otazka. Oba zpusoby maji svoje pro/proti a je to hodne veci v kusu. (Nekde jsem cel, ze velke pismenka v tomto pripade pritahuji zbytecne moc pozornosti na neco co neni az tak dulezite, ale je to opravdu vec nazoru.)
> #### Zaver: 
> Budeme pouzivat `PascalCase`.

12. ![#32CD32](https://placehold.it/15/32CD32/000000?text=+) `100%` - Vždy když je to relevantní, píšeme `nameof(...)` místo `"..."`.
13. ![#FFFF00](https://placehold.it/15/FFFF00/000000?text=+) `60%` - Délka jednoho řádku nepřesahne 150 znaků. (*Testovácí projekty mají vyjímku, neboť se vnich často použivají dlouhe názvy metod apod.* )

> #### Reakce:
> * *proč 150? přijde mi, že současné monitory v pohodě dovolí i více*  
> * *Tohle je spíše k diskuzi. Podle mě není dobré definovat přesnou délku jednoho řádku.*  
> * *Visual Studio má v nastavení "word wrap". takže každý, komu vadí dlouhý řádek si ho může nechat vizuálně zalomit*
> #### Odpoved:
> Osobne si myslim ze to ma vyznam z nekolika duvodu:
> 1. Dlouhy radek je podle me potencialni "code smell" (Metoda s prilis dlouhymi parametry, ...).
> 2. I kdyz monitory dovoluji vice, nemyslim si ze vice znaku na radek znas udela lepsi programatory a zcitatelni kod. Navic obcas musi clovek programovat na notebooku bez externiho 27 palcoveho monitoru.
> 3. Pokud si delame navzajem CodeReview v devopsech nebo jinych nastrojich kde mame side by side stary a novy kod, je toho mista na cteni mene. (Toto "Word wrap" nevyresi.)  
> #### Zaver:
> Tento bod prozatim zustava, pokud nas bude prilis omezovat, da se casem upravit/zrusit.

14. ![#FFFF00](https://placehold.it/15/FFFF00/000000?text=+) `75%` - Při zalamování řádku, operátoru `.`, `=>`, `?:`, `&&` dáváme na začátek následujícího a ne na konec předešlého. (Vyjímka je pro operátor `=>` jestliže je použitý v parametru metody, která je lambda funkcí.).

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

> #### Reakce:
> *Nevidím důvod k tomu, abychom striktně určovali, jestli operátor patří na konec řádku, nebo na začátek řádku dalšího.*  
> #### Odpoved:
> Je to jeden z castych specifikovanych bodu.
> #### Zaver: 
> Tento bod nechame tak jak je.

15. ![#32CD32](https://placehold.it/15/32CD32/000000?text=+) `100%` - Obecně se snažíme nepoužívat komentaře v našem běžném kódu. Pokud už takový komentář napíšu musí jasně říkat **proč** je tento řádek okomentován. (Dokumentační komentáře veřejných věcí používáme podle potřeby.)
> #### Zaver: 
> Zkusim tento bod preformuloval a nebo pribudne dalsi obsahujici nejake blizsi info o namingu. (Viz. Dodatky)

16. ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) `50%` - Všechny `private` proměnné definujeme na začátku třídy. `Protected` a `public` se deklarují až po konstruktorech.

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
> #### Reakce:
> * *Jsem pro zavedeni hierarchie ve stylu "constructor, public, protected, private" v obou smerech*  
> * *Tohle mi přijde extra nepřehledné. Všude píšem všechne fieldy/property nad konstruktor.*  
> * *Nesouhlasím. Proč bychom měli protected a public členy deklarovat až pod konstruktorem a private nad ním? Nedává mi to smysl. Myslím si, že data inicializované v konstrutoru by měly být nad ním bez ohledu na jejich modifikátor přístupu.*
>  * *Mám na to jiný pohled: Shora nejdříve public, pod ně private a pak konstruktor.*
> #### Odpoved:
> StyleCop ([Wiki](https://en.wikipedia.org/wiki/StyleCop), [Github](https://github.com/DotNetAnalyzers/StyleCopAnalyzers/blob/master/DOCUMENTATION.md)), Resharper, aj. Maji v tomto bodu nasledujici defaultni konvenci:
```
Within a class, struct, or interface, elements must be positioned in the following order:
    Constant Fields
    Fields
    Constructors
    Finalizers (Destructors)
    Delegates
    Events
    Enums
    Interfaces
    Properties
    Indexers
    Methods
    Structs
    Classes
Elements of the same type must be positioned in the following order by access level:
    public
    internal
    protected internal
    protected
    private
```
> #### Zaver:
> V nasi praxi se nevyskytuji tridy, ktere by byly takto "silene" a obsahovaly tolik casti.  
> Tento bod zatim vyskrtneme a nebudeme ho striktne definovat.  
> Obecne plati ze metody jsou pod konstruktorem v poradi, public -> internal -> ... -> private. Property a fieldy nad konstruktor.


## DODATKY

> #### 1. :
> *chybí mi bod, který říká, jestli budeme používat podtržítko pro privátní členy nebo jenom privátní readonly členy.*  
> #### Odpoved:
> Bod 3 - Podtrzitko nepouzivame. Bude tam doplnen spatny priklad aby to bylo jasne.

> #### 2. :
> *Doplnil bych řazení metod ve třídě. Nejvýše public, níže protected, poté private. Vše pod konstruktorem*  
> #### Odpoved:
> Dobry poznatek, stane se to asi nepsanym pravidlem. Pokud bude potreba dopiseme.

> #### 3. :
> *Co se týče názvů tabulek (jednotné/mn. číslo), název modelu zase jednotné číslo.*  
> #### Odpoved:
> Mas pravdu, asi nepokryjeme veskere pripady ale bod 15 zkusime upravit aby rikal ze se snazime pojmenovavat veci dobre, k cemuz patri i spravne pouzivani jednotneho a mnozneho cisla.

> #### 4. :
> *Používání vnořených funkcí: Používat pouze v případě, kdy je to opravdu vhodné/nutné.*  
> #### Odpoved:
> Ano. Pevne verim ze vnorene funkce nikdo nejak agresivne nepouziva. Zatim bych tento bod neuvadel.

> #### 5. :
> *Pojmenování proměnných: Souvisí to s nepouživáním komentářů. Pojmenování proměnných by mělo být jasné, aby byl kód čitelný a nemusely se používat komentáře.*  
> #### Odpoved:
> Dobry postreh, zkusim preformulovat myslenku 15 aby obsahovala i tuto myslenku.

> #### 6. :
> *Přidal bych ještě pravidla pojmenovávání metod a proměnných.*  
> #### Odpoved:
> Souhlasim. Zkusim lepe zformulovat 15. Podle me to souvisi i s komentari. Dobry naming = komentare jsou zbytecne.
