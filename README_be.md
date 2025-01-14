# Стандартная структура праекта Go

Пераклады:

* [한국어 문서](README_ko.md)
* [简体中文](README_zh.md)
* [正體中文](README_zh-TW.md)
* [简体中文](README_zh-CN.md) - ???
* [Français](README_fr.md)
* [日本語](README_ja.md)
* [Português](README_ptBR.md)
* [Español](README_es.md)
* [Română](README_ro.md)
* [Русский](README_ru.md)
* [Türkçe](README_tr.md)
* [Italiano](README_it.md)
* [Vietnamese](README_vi.md)
* [Українська](README_ua.md)
* [Indonesian](README_id.md)
* [हिन्दी](README_hi.md)
* [فارسی](README_fa.md)
* [Беларуская](README_be.md)

## Агляд

Гэта базавая структура для праектаў праграм на Go. Звярніце ўвагу, што яна базавая з пункту гледжання зместу, бо канцэнтруецца толькі на агульнай структуры, а не тым, што ўнутры. Яна таксама базавая таму, што вельмі высокага ўзроўню і не паглыбляецца ў дэталі таго, як можна яшчэ больш структуравана арганізаваць ваш праект. Напрыклад, яна не спрабуе ахапіць структуру на ўзор чагосьці накшталт Чыстай Архітэктуры.

Гэта **`НЕ афіцыйны стандарт, вызначаны асноўнай камандай распрацоўшчыкаў Go`**. Гэта набор агульных гістарычных і новых шаблонаў размяшчэння праектаў у экасістэме Go. Некаторыя з гэтых шаблонаў больш папулярныя за іншыя. Ён таксама ўключае шэраг невялікіх удасканаленняў разам з некалькімі дапаможнымі каталогамі, якія звычайна сустракаюцца ў любым дастаткова вялікай рэальнай праграме. Звярніце ўвагу, што асноўная **каманда Go дае выдатны набор агульных рэкамендацый па структурыраванні праектаў на Go** і што гэта азначае для вашага праекта пры яго імпарце і ўсталёўцы. Глядзіце старонку [`Арганізацыя модуля Go`](https://go.dev/doc/modules/layout) ў афіцыйнай дакументацыі Go для больш падрабязнай інфармацыі. Яна ўключае ўзоры каталогаў `internal` і `cmd` (апісаныя ніжэй) і іншую карысную інфармацыю.

**`Калі вы спрабуеце вывучыць Go або ствараеце PoC ці просты праект для сябе, гэтая структура праекта з'яўляецца празмернасцю. Пачніце з чагосьці сапраўды простага (адзін `main.go` файл і `go.mod` больш чым дастаткова).`**  Па меры росту вашага праекта памятайце, што важна пераканацца, што ваш код добра структураваны, у адваротным выпадку вы атрымаеце блытаны код з мноствам схаваных залежнасцей і глабальным станам. Калі над праектам будзе працаваць больш людзей, вам спатрэбіцца яшчэ большая структура. Вось тады важна ўвесці агульны спосаб кіравання пакетамі/бібліятэкамі. Калі ў вас ёсць праект з адкрытым зыходным кодам або вы ведаеце што іншыя праекты імпартуюць код з рэпазіторыя вашага праекта - вось тады важна мець прыватныя (`internal`) пакеты і код. Кланіруйце рэпазіторый, захавайце тое, што вам трэба і выдаліце ўсё астатняе! Толькі таму што яно там ёсць не азначае што вам усё гэта патрэбна. Ніводзен з гэтых шаблонаў не выкарыстоўваецца ва ўсіх без выключэннях праектах. Нават шаблон `vendor` не універсальны.

З Go 1.14 [`Go Modules`](https://go.dev/wiki/Modules) нарэшце гатовыя да ўжытку. Выкарыстоўвайце [`Go Modules`](https://blog.golang.org/using-go-modules), калі ў вас няма канкрэтнай прычыны не выкарыстоўваць іх, а калі і ёсць, то вам не трэба турбавацца пра $GOPATH і дзе размясціць ваш праект. Асноўны файл `go.mod` у рэпазіторыі разлічвае, што ваш праект размешчаны на GitHub, але гэта не абавязковае патрабаванне. Шлях модуля можа быць любым, хоць першы кампанент шляху модуля павінен мець кропку ў сваёй назве (цяперашняя версія Go больш гэтага не патрабуе, але калі вы карыстаецеся крыху старэйшымі версіямі - не здзіўляйцеся, калі сабраць праект без яе не ўдасца). Глядзіце Issues [`37554`](https://github.com/golang/go/issues/37554) і [`32819`](https://github.com/golang/go/issues/32819) для дадатковай інфармацыі.

Гэты шаблон праекта наўмысна агульны і не спрабуе навязаць канкрэтную структуру пакета Go.

Гэта намаганне супольнасці. Адкрыйце issue, калі знойдзеце новы ўзор або лічыце, што адзін з існуючых трэба абнавіць.

Калі вам патрэбна дапамога з назвай, фарматаваннем і стылямі, пачніце з запуску [`gofmt`](https://golang.org/cmd/gofmt/) і [`staticcheck`](https://github.com/dominikh/go-tools/tree/master/cmd/staticcheck). Папярэдні стандартны лінтар golint цяпер састарэў і не падтрымліваецца; рэкамендуецца выкарыстоўваць лінтар які падтрымліваецца, такі як staticcheck. Таксама пераканайцеся, што вы прачыталі гэтыя стайлгайды для Go:
* https://talks.golang.org/2014/names.slide
* https://golang.org/doc/effective_go.html#names
* https://blog.golang.org/package-names
* https://go.dev/wiki/CodeReviewComments
* [Кіраўніцтва па стылі для пакетаў Go](https://rakyll.org/style-packages) (rakyll/JBD)

Глядзіце [`шаблон праекта Go`](https://medium.com/golang-learn/go-project-layout-e5213cdcfaa2) для дадатковай інфармацыі.

Больш пра найменне і арганізацыю пакетаў, а таксама іншыя рэкамендацыі па структуры кода:
* [GopherCon EU 2018: Пітэр Бургон - Лепшыя практыкі для прамысловага праграмавання](https://www.youtube.com/watch?v=PTE4VJIdHPg)
* [GopherCon Russia 2018: Эшлі МакНамара + Браян Кетэльсэн - Лепшыя практыкі Go](https://www.youtube.com/watch?v=MzTcsI6tn-0)
* [GopherCon 2017: Эдвард Мюлер - Анты-шаблоны ў Go](https://www.youtube.com/watch?v=ltqV6pDKZD8)
* [GopherCon 2018: Кат Зіен - Як структуравать вашы Go прыкладанні](https://www.youtube.com/watch?v=oL6JBUk6tj0)

Кітайскі пост пра прынцыпы Package-Oriented-Design і архітэктурны слой
* [Пакетна-арыентаваны дызайн і архітэктурнае напластаванне](https://github.com/danceyoung/paper-code/blob/master/package-oriented-design/packageorienteddesign.md)

## Go каталогi

### `/cmd`

Асноўныя прымяненні для гэтага праекта.

Назва каталога для кожнай праграмы павінна адпавядаць назве выканальнага файла (напрыклад, `/cmd/myapp`).

Не змяшчайце шмат кода ў каталог праграмы. Калі вы лічыце, што код можна імпартаваць і выкарыстоўваць у іншых праектах, ён павінен знаходзіцца ў каталогу `/pkg`. Калі код не можа быць паўторна выкарыстаны або калі вы не хочаце, каб іншыя яго выкарыстоўвалі, змясціце гэты код у каталог `/internal`. Вы бы здзівіліся, што іншыя бы зрабілі, таму ясна выражайце свае намеры!

Распаўсюджаная практыка мець невялікую `main` функцыю, якая імпартуе і выклікае код з каталогаў `/internal` і `/pkg`, і больш нічога.

Прыклады ў каталогу [`/cmd`](cmd/README.md).

### `/internal`

Прыватны код праграмы і бібліятэкі. Гэта код, які вы не хочаце, каб іншыя імпартавалі ў свае праграмы або бібліятэкі. Звярніце ўвагу, што гэты шаблон размяшчэння забяспечваецца самім кампілятарам Go. Глядзіце [`нататкі да выпуску`](https://golang.org/doc/go1.4#internalpackages) Go 1.4 для больш падрабязнай інфармацыі. Заўважце, што вы не абмежаваныя толькі верхнім узроўнем `internal` каталога. Вы можаце мець больш за адзін `internal` каталог на любым узроўні вашага дрэва праекта.

Вы можаце дадаткова дадаць трохі структуры ў вашы ўнутраныя пакеты, каб аддзяліць агульны і неагульны ўнутраны код. Гэта не абавязкова (асабліва для меншых праектаў), але прыемна мець візуальныя падказкі, якія паказваюць на запланаванае выкарыстанне пакета. Ваш фактычны код праграмы можа знаходзіцца ў каталогу `/internal/app` (напрыклад, `/internal/app/myapp`), а код, які выкарыстоўваецца гэтымі праграмамі - у каталогу `/internal/pkg` (напрыклад,`/internal/pkg/myprivlib`).

Вы выкарыстоўваеце `internal` каталогі, каб зрабіць пакеты прыватнымі. Калі вы размяшчаеце пакет унутры `internal` каталога, то іншыя пакеты не могуць яго імпартаваць, калі яны не маюць агульнага продка. І гэта адзіны каталог, названы ў дакументацыі Go, які мае спецыяльную апрацоўку кампілятарам.

### `/pkg`

Код бібліятэкі, які могуць выкарыстоўваць знешнія праграмы (напрыклад, `/pkg/mypubliclib`). Іншыя праекты будуць імпартаваць гэтыя бібліятэкі, разлічваючы на іх працу, таму двойчы падумайце перад тым, як размясціць тут нешта 😃 Звярніце ўвагу, што `internal` каталог - лепшы спосаб забяспечыць недаступнасць вашых прыватных пакетаў для імпарту, бо гэта забяспечваецца Go. Каталог `/pkg` па-ранейшаму добры спосаб выразна паведаміць аб бяспецы кода ў гэтым каталогу для выкарыстання іншымі. Блог-паведамленне [`I'll take pkg over internal`](https://travisjeffery.com/b/2019/11/i-ll-take-pkg-over-internal/) Трэвіса Джэферы дае добры агляд каталогаў `pkg` і `internal` і калі ёсць сэнс іх выкарыстоўваць.

Гэта таксама спосаб згрупаваць код Go ў адным месцы, калі ваш каранёвы каталог утрымлівае шмат не-Go кампанентаў і каталогаў, што палягчае запуск розных інструментаў Go (як згадваецца ў гэтых дакладах: [`Лепшыя практыкі для прамысловага праграмавання`](https://www.youtube.com/watch?v=PTE4VJIdHPg) з GopherCon EU 2018, [`GopherCon 2018: Кат Зіен - Як структураваны вашы праграмы на Go`](https://www.youtube.com/watch?v=oL6JBUk6tj0) і [`GoLab 2018 - Масімільяна Піппі - Шаблоны размяшчэння праектаў у Go`](https://www.youtube.com/watch?v=3gQa1LWwuzk)).

Калі вы хочаце ўбачыць, якія папулярныя рэпазіторыі Go выкарыстоўваюць гэты шаблон праекта, паглядзіце каталог [`/pkg`](pkg/README.md). Гэта распаўсюджаны шаблон, але ён не з'яўляецца агульнапрынятым і некаторыя ў супольнасці Go яго не рэкамендуюць.

Гэта нармальна не выкарыстоўваць яго, калі ваш праект сапраўды невялікі і дадатковы ўзровень ўкладання не моцна дапамагае (калі толькі вы сапраўды гэтага не хочаце 😃). Падумайце пра гэта, калі ён становіцца дастаткова вялікім і ваша каранёвая дырэкторыя становіцца даволі загружанай (асабліва калі ў вас ёсць шмат кампанентаў праграмы, якія не на Go).

Паходжанне каталога `pkg`: стары зыходны код Go выкарыстоўваў `pkg` для сваіх пакетаў, і тады розныя праекты Go ў супольнасці пачалі капіяваць гэты шаблон (больш кантэксту ў [`твітах`](https://twitter.com/bradfitz/status/1039512487538970624) Брэда Фіцпатрыка).

### `/vendor`

Залежнасці праграмы (кіруюцца ўручную або з дапамогай вашага любімага інструмента кіравання залежнасцямі, як новая ўбудаваная функцыя [`Go Modules`](https://go.dev/wiki/Modules)). Каманда `go mod vendor` створыць для вас каталог `/vendor`. Звярніце ўвагу, што вам можа спатрэбіцца дадаць сцяг `-mod=vendor` у вашу каманду `go build`, калі вы не выкарыстоўваеце Go 1.14, дзе ён перадвызначаны.

Не ўключайце залежнасці вашай праграмы, калі ствараеце бібліятэку.

Звярніце ўвагу, што з версіі [`1.13`](https://golang.org/doc/go1.13#modules) Go таксама ўключыў функцыю проксі-модуля (выкарыстоўваючы [`https://proxy.golang.org`](https://proxy.golang.org) у якасці перадвызначанага сервера проксі-модуля). Прачытайце больш пра гэта [`тут`](https://blog.golang.org/module-mirror-launch), каб даведацца, ці адпавядае гэта ўсім вашым патрабаванням і абмежаванням. Калі так, то каталог `vendor` увогуле не спатрэбіцца.

## Каталогі cервісных праграм

### `/api`

Спецыфікацыі OpenAPI/Swagger, файлы схем JSON, файлы вызначэння пратаколаў.

Прыклады ў каталогу [`/api`](api/README.md).

## Каталогі вэб-праграм

### `/web`

Кампаненты, спецыфічныя для вэб-праграм: статычныя файлы, шаблоны для апрацоўкі з боку сервера і SPA (аднастаронкавыя праграмы).

## Агульныя каталогі праграм

### `/configs`

Шаблоны файлаў канфігурацыі або стандартныя канфігурацыі.

Cвае файлы шаблонаў размясціце ў `confd` або `consul-template`.

### `/init`

Канфігурацыі ініцыялізацыі сістэмы (systemd, upstart, sysv) і менеджара/наглядчыка працэсаў (runit, supervisord).

### `/scripts`

Скрыпты для выканання розных аперацый зборкі, ўсталёўкі, аналізу і г.д.

Гэтыя скрыпты пакідаюць файл каранёвы Makefile маленькім і простым (напрыклад, [`https://github.com/hashicorp/terraform/blob/main/Makefile`](https://github.com/hashicorp/terraform/blob/main/Makefile)).

Прыклады ў каталогу [`/scripts`](scripts/README.md).

### `/build`

Зборка і бесперапынная інтэграцыя (Continuous Integration, CI).

Змясціце вашыя канфігурацыі і скрыпты пакетаў воблака (AMI), кантэйнера (Docker), аперацыйнай сістэмы (deb, rpm, pkg) у каталогу `/build/package`.

Змясціце вашы канфігурацыі і скрыпты CI (travis, circle, drone) у каталогу `/build/ci`. Звярніце ўвагу, што некаторыя інструменты CI (напрыклад, Travis CI) вельмі капрызныя да размяшчэння сваіх файлаў канфігурацыі. Cпрабуйце змясціць файлы канфігурацыі ў каталогу `/build/ci` з спасылкай на месца, дзе інструменты CI чакаюць іх знайсці (калі гэта магчыма).

### `/deployments`

IaaS, PaaS, канфігурацыі разгортвання аркестрацыі сістэм і кантэйнераў і шаблоны (docker-compose, kubernetes/helm, terraform). Звярніце ўвагу, што ў некаторых рэпазіторыях (асабліва праграмах, разгорнутых з дапамогай kubernetes) гэты каталог называецца `/deploy`.

### `/test`

Дадатковыя знешнія тэставыя праграмы і тэставыя даныя. Вы можаце свабодна структуравать каталог `/test` так, як вам зручна. Для большых праектаў мае сэнс мець падкаталог для даных. Напрыклад, вы можаце мець `/test/data` або `/test/testdata`, калі вам трэба, каб Go ігнараваў тое, што знаходзіцца ў гэтым каталогу. Звярніце ўвагу, што Go таксама будзе ігнараваць каталогі або файлы, якія пачынаюцца з "." або "_", таму ў вас ёсць большая гнуткасць у тым, як называць ваш каталог тэставых даных.

Прыклады ў каталогу [`/test`](test/README.md).

## Other Directories

### `/docs`

Дызайн і дакументы карыстальніка (у дадатак да вашай дакументацыі, згенераванай godoc).

Прыклады ў каталогу [`/docs`](docs/README.md).

### `/tools`

Інструменты падтрымкі для гэтага праекта. Звярніце ўвагу, што гэтыя інструменты могуць імпартаваць код з каталогаў `/pkg` і `/internal`.

Прыклады ў каталогу [`/tools`](tools/README.md).

### `/examples`

Прыклады для вашых праграм і/або публічных бібліятэк.

Прыклады ў каталогу [`/examples`](examples/README.md).

### `/third_party`

Знешнія дапаможныя інструменты, раздвоены код і іншыя зьнешнія ўтыліты (напрыклад, Swagger UI).

### `/githooks`

Git хукі.

### `/assets`

Іншыя файлы, якія суправаджаюць ваш рэпазітарый (малюнкі, лагатыпы і г.д.).

### `/website`

Гэта месца для размяшчэння даных вашага праекта, калі вы не выкарыстоўваеце GitHub Pages.

Прыклады ў каталогу [`/website`](website/README.md).

## Каталогі, якіх у вас не павінна быць

### `/src`

Некаторыя праекты на Go сапраўды маюць тэчку `src`, але гэта звычайна адбываецца, калі распрацоўшчыкі прыйшлі з Java-свету, дзе гэта агульная схема. Калі не цяжка, паспрабуйце не прымаць гэты шаблон Java. Вы сапраўды не хочаце, каб ваш код на Go або праекты на Go выглядалі як Java 😃

Не блытайце каталог `/src` на ўзроўні праекта з каталогам `/src`, які Go выкарыстоўвае для сваіх працоўных асяроддзяў, як апісана ў [`Як пісаць код на Go`](https://golang.org/doc/code.html). Зменная асяроддзя `$GOPATH` паказвае на ваша (цяперашняе) працоўнае асяроддзе (перадвызначана яна паказвае на `$HOME/go` у не-Windows сістэмах). Гэтае працоўнае асяроддзе ўтрымлівае верхнеўзроўневыя каталогі `/pkg`, `/bin` і `/src`. Ваш фактычны праект становіцца падкаталогам унутры `/src`, таму калі ў вас ёсць каталог `/src` у вашым праекце, шлях да праекта будзе выглядаць так: `/some/path/to/workspace/src/your_project/src/your_code.go`. Заўважце, што пачынаючы з Go 1.11 можна мець свой праект па-за межамі `GOPATH`, але гэта ўсё роўна не робіць гэты шаблон размяшчэння добрым.

## Значкі

* [Go Report Card](https://goreportcard.com/) - праскануе ваш код праз `gofmt`, `go vet`, `gocyclo`, `golint`, `ineffassign`, `license` і `misspell`. Замяніце `github.com/golang-standards/project-layout` на спасылку на ваш праект.

    [![Go Report Card](https://goreportcard.com/badge/github.com/golang-standards/project-layout?style=flat-square)](https://goreportcard.com/report/github.com/golang-standards/project-layout)

* ~~[GoDoc](http://godoc.org) - забяспечыць анлайн-версію вашай дакументацыі, створанай з дапамогай GoDoc. Змяніце на спасылку на ваш праект.~~

    [![Go Doc](https://img.shields.io/badge/godoc-reference-blue.svg?style=flat-square)](http://godoc.org/github.com/golang-standards/project-layout)

* [Pkg.go.dev](https://pkg.go.dev) - Pkg.go.dev - гэта новае месца для пазнавання і дакументацыі Go. Вы можаце стварыць значок, выкарыстоўваючы [інструмент генерацыі значкоў](https://pkg.go.dev/badge).

    [![PkgGoDev](https://pkg.go.dev/badge/github.com/golang-standards/project-layout)](https://pkg.go.dev/github.com/golang-standards/project-layout)

* Release - пакажа апошні нумар рэлізу для вашага праекта. Змяніце спасылку на GitHub на ваш праект.

    [![Release](https://img.shields.io/github/release/golang-standards/project-layout.svg?style=flat-square)](https://github.com/golang-standards/project-layout/releases/latest)

## Нататкі

Больш смелы шаблон праекта з узорамі, паўторна выкарыстоўваемымі канфігурацыямі, скрыптамі і кодам знаходзіцца ў распрацоўцы.