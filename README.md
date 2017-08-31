# Application in C# for collecting data from LEGO MINDSTORM EV3
Tato verze nemusí být zcela aktuální, podrobnější dokumentaci naleznete v souboru Jan_Menšík.pdf
# Cíl projektu
Tento projekt bude primárně zaměřen a konstruován pro sběr dat z portů Lego robota EV3. Program bude naprogramovaný pomocí programu Microsoft Visual Studio na platformě .NET 4.5 . Program bude komunikovat přes bluetooth a jeho výstupem budou textové soubory s uloženými daty. Program bude vyvíjen v jazyce C#.
 
# Obsah Programu
Po spuštění programu se připojíme na robota EV3 (robota EV3 musíte spárovat s Vaším počítačem), 
To uděláme tak že si v levém horním rohu vybereme bluetooth COM port a následně klikneme na tlačítko Connect.

Pokud se program správně připojí, robot vydá zvukové znamení. Po připojení čidel do portů (1,2,3,4) nebo motorů do portů (A,B,C,D), program zobrazuje aktuální hodnoty na daných portech.
 
Pro zaznamenání požadovaných dat z vybraného portu robota, klikněte na tlačítko „Záznam“ u požadovaného portu. Pokud budete chtít ukončit záznam, kliknete na tlačítko „Stop“ u vybraného portu. Probíhající záznam uživatel pozná z červeně zbarvené hodnoty u portu.
 
# Tutoriál
Tento tutoriál Vás seznámí se zdrojovým kódem programu, jeho knihovnami a také si ukážeme jak se připojit k EV3 pomocí bluetooth.
Připojení
Pro připojení robota butete potřebovat Lego „brick“ EV3. Pro bluetooth komunikaci musí mít robot v nastavení zapnutý bluetooth visibility a vypnutou bluetooth komunikaci s iPhone/iPad/iPod. Dále je potřeba mít nainstalovaný vývojové prostředí Microsoft Visual Studio s platformou .NET 4.5 . 
Robota nejprve přes bluetooth spárujeme, defaultní heslo je „1234“. Po spárování můžeme přistoupit k tvorbě projektu. Nejprve zvolíme vytvořit nový projekt, jako programovací jazyk zvolíme Visual C# a vybereme Windows Presentation Foundation client application. 
Po načtení vybereme v okně Solution Explorer položku References a přidáme knihovnu s názvem „Lego.EV3.Desktop“. Do „MainWindow.xaml.cs“ přidáme tyto importy :

using Lego.Ev3.Core;
using Lego.Ev3.Desktop;
 To nám umožní komunikaci s přidanou knihovnou „Lego.EV3.Desktop“. Více o této knihovně naleznete na [1].  V souboru „MainWindow.xaml“ si klikneme na plátno a v panelu Properties rozklikneme pole pro hodnotu, to nám přidá metodu která se provede po načtení okna.
 
 
Vytvoříme si kostku private Brick brick; v hlavní třídě. Do metody „Window_Loaded“ přidáme příkaz pro připojení k COM portu, kde se nachází odchozí spojení pro EV3, například : 
    brick = new Brick(new BluetoothCommunication(„COM1“)); // COM1 značí odchozí port
    await brick.ConnectAsync(); // pro asynchronní přípojení
    await brick.DirectCommand.PlayToneAsync(100, 1000, 300); // EV3 spustí tón

       
Po spuštění se aplikace napojí na EV3 a robot vyšle pronikavý tón. 
Pro přidání tlačítka si otevřeme designer v souboru „MainWindow.xaml“, vybereme si Toolbox a přetáhneme si na plátno Button. V properties můžeme různě upravovat jeho vzhled, nebo měnit název. Po kliknutí na tlačítko se nám vytvoří nová metoda, díky které můžeme tlačitku přidat akci, která se provede při kliknutí na tlačítko za běhu aplikace. 
Dále bych mohl čtenáře seznámit se všemi možnostmi EV3 API, ale tyto informace už jsou mimo obsah této práce.
 
# Literatura
[1]	Brian Peek : Getting Started Guide. https://github.com/BrianPeek/legoev3/wiki 

# Závěr
Tento projekt jsem si vybral jak ze zájmu o robotiku, tak z možnosti se naučit novým jazykům. Proto byl pro vývoj vybrán .NET, protože jsem s touto platformou ještě neměl žádné zkušenosti. V aplikaci lze přizpůsobit výstup.

Webová aplikace pro příjem dat ✔

Implementace zobrazení grafu přímo v aplikaci 

Vytvoření intuitivnějšího rozhraní.  ✔
