# Cvičení: Úkolníček - context

Pokračujeme s aplikací Úkolníček, ve které jsme v předchozím cvičení předali data z formuláře do hlavní App, která je uložila do stavu a tím se nový úkol objevil v seznamu úkolů.

V tak jednoduché aplikaci, jako je náš Úkolníček, je použití React Contextu tak trochu "overkill", ale i tak nám to může nějaké výhody přinést, tak6e si context do aplikace přidáme.

1. Vytvoř si složku `context` a v ní založ soubor `tasks-context.tsx`.
2. V souboru naimportuj vše potřebné a vytvoř nový context, nazvi ho třeba `TaskContext`.
3. Context naimportuj do `App` a zabal veškerý HTML obsah komponenty do **provideru**. Jako výchozí hodnotu provideru dej objekt, který zatím bude obsahovat jedinou vlastnost `tasks`, jejíž hodnota bude pole s úkoly, které máme uložené ve stavu.
4. Uprav aplikaci tak, aby se úkoly do komponenty `List` nepředávaly jako parametry, ale aby si je komponenta místo toho sama načítala z contextu. Budeš muset upravit typy pro komponenty.
5. Vyzkoušej, že po všech těchto úpravách dělá aplikace přesně to stejné, co na začátku dělala i bez bez těchto úprav 🙈
6. V hlavní `App` vytvoř funkci `addTask`, která jako parametr bude přijímat objekt s názvem a popisem úkolu, a přidá ho stavu se seznamem úkolů. V podstatě stačí, když přejmenuješ funkci, kterou jsme v předchozím cvičení přidali, aby reagovala na odeslání formuláře v komponentě `Form`.
7. Předávání funkce do `Form` přes props už nebudeme potřebovat, takže ho zrušte. Místo toho přidejte funkci `addTask` do kontextu. V komponentě `Form` si z kontextu funkci získejte a volejte ji při odeslání formuláře.

## BONUS
8. V hlavní `App` přidej i funkci `deleteTask`, která určený úkol smaže (asi podle indexu v poli). Funkci přidej do kontextu a zařiď, aby se v komponentě `Task` z kontextu získala. Přidej do úkolu tlačítko (nebo ikonku, apod.), které po kliknutí funkci zavolá a úkol se smaže.
9. Udělěj to stejné, jako v předchozím bodu, ale pro funkci `markTaskDone`, která úkol označí jako hotový (nebo pokud je hotový, tak ho označí zpět jako nehotový).
