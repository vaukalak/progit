# Першыя крокі #

Гэтая глава пра тое, як пачаць працу з Git. Спачатку мы растлумачым асновы інструмэнтаў кіраваньня вэрсіямі, затым разьбяромся як атрымаць працоўны Git на сваёй сістэме і, урэшце, як наладзіць яго так, каб зь ім можна было пачаць працаваць. Напрыканцы гэтае главы вы будзеце разумець для чаго наогул прызначаны Git, чаму ім варта карыстацца і будзеце умець наладжваць яго.

## Пра кіраваньне вэрсіямі ##

Што такое кіраваньне вэрсіямі і навошта яно патрэбнае? Кіраваньне вэрсіямі — гэта сістэма, якая запісвае зьмены, што адбыліся з файлам ці наборам файлаў зь цягам часу, так каб потым вы маглі бачыць патрэбныя старыя вэрсіі. У прыкладах гэтай кнігі мы будзем працаваць з зыходнымі кодамі праграм, але, насамрэч, вы можаце працаваць практычна з любымі тыпамі файлаў, якія існуюць на вашым кампутары.

Калі вы графічны ці вэб-дызайнер і маеце намер захоўваць кожную вэрсію малюнкаў ці слаёў (што вам больш патрэбна), то выкарыстаньне сістэмы кіраваньня вэрсіямі (СКВ; Version Control System, VCS) гэта вельмі разумны выбар. Гэта дазволіць вам вярнуць файлы да папярэдняга стану, вярнуць да папярэдняга стану увесь праект, параўнаць змены паміж рознымі станамі, убачыць хто апошнім змяняў нешта, што можа выклікаць праблемы, хто прапанаваў змену і калі, і шмат іншага. Выкарыстаньне СКВ у асноўным значыць, што калі вы сапсавалі нешта ці страцілі файлы, то гэта можна лёгка аднавіць. Як дадатак, гэта не запатрабуе вялікіх намаганьняў і выдаткаў з вашага боку.  

### Лакальныя сістэмы кіраваньня вэрсіямі ###

Шмат людзей ў якасьці мэтаду кіраваньня вэрсіямі выбірае капіяваньне файлаў у іншую тэчку (магчыма, з датай у назве, калі чалавек досыць разумны). Гэты падыход вельмі распаўсюджаны з-за сваёй прастаты, але ён пакідае неверагодна шмат магчымасьцяў для памылак. Вельмі лёгка забыцца ў якой тэчцы вы зараз і выпадкова запісаць ня ў той файл, ці зкапіяваць зусім не туды, куды вы зьбіраліся.

Каб вырашыць гэтую праблему праграмісты шмат часу таму распрацавалі лакальныя СКВ, якія выкарыстоўваюць простую базу дадзеных каб захоўваць ўсе змены ў файлах, вэрсіі якіх адсочваюцца (гл. Малюнак 1-1).

Insert 18333fig0101.png 
Малюнак 1-1. Сьхема лакальнага кіраваньня вэрсіямі.

Адной з папулярных у той час СКВ была rcs, якая ўсё яшчэ пастаўляецца з вялікай колькасцю кампутараў. Нават папулярная аперацыйная сістэма Mac OS X усталёўвае rcs у складзе пакета Developer Tools. Праца гэтай прылады заснаваная на захаванні на дыску ў спецыяльным фармаце набораў латак (patch) (гэта запісы розніцы паміж дзвума файламі) для кожнай змены файла. Гэта дапамагае вярнуць файл да любога з зафіксаваных станаў, паслядоўна накладыючы латкі адну за адной.

### Цэнтралізаваныя сістэмы кантролю версій ###

Наступнай сур'ёзнай праблемай, з якой людзі сутыкнуліся была неабходнасць супрацоўнічаць з распрацоўшчыкамі за іншымі кампутарамі. Централізаваныя сістэмы кантролю версій (ЦСКВ) былі распрацаваныя каб развязаць гэтую праблему. Такія сістэмы як CVS, Subversion і Perforce складаюцца з сервера, на якім захоўваюцца ўсе дадзеныя па версіях файлаў, і некаторай колькасці кліенцкіх машын, якія атрымліваюць файлы з сервера. Шмат год такая схема з'яўлялася стандартам кантролю версій (гл. Малюнак 1-2).

Insert 18333fig0102.png 
Малюнак 1-2. Схема цэнтралізаванага кантролю версій.

Гэты падыход мае шмат пераваг, асабліва ў параўнанні з лакальнымі СКВ. Напрыклад, усе дакладна ведаюць што астатнія робяць і што наогул адбываецца ў праекце. Адміністратары маюць зручную магчымасць кантролю за тым хто што можа зрабіць. І гэта значна прасцей, чым адміністраванне лакальных баз дадзеных СКВ на кожнай кліенцкай машыне.

Аднак, гэты падыход мае і некаторыя сур'ёзныя мінусы. Самы відавочны з іх — центральны сервер яўляе сабою пункт, крах якога цягне за сабою крах усёй сістэмы. Калі гэты сервер спыніць працу на гадзіну — у гэтую гадзіну ніхто не зможа абмяняцца з супрацоўнікамі вынікамі сваёй працы ці захаваць новую версію таго, над чым ён ці яна зараз працуе. Калі жосткі дыск, на якім змешчаная цэнтральная база дадзеных пашкоджаны, а актуальных рэзервовых копій няма, то вы згубіце абсалютна ўсё: усю гісторыю праекту, за выключэннем тых здымкаў, што карыстальнікі выпадкова мелі на сваіх лакальных кампутарах. Лакальныя СКВ пакутуюць на тую ж праблему: калі ты маеш усю гісторыю праекта толькі ў адным месцы, то ты рызыкуеш згубіць усё.

### Размеркаваныя сістэмы кантролю версій ###

І вось тут у гульню ўступаюць размеркаваныя сістэмы кантролю версій (РСКВ). У РСКВ (такіх як Git, Mercurial, Bazaar ці Darcs) кліенты не толькі атрымліваюць апошнія здымкі файлаў: яны атрымліваюць поўную копію сховішча. Такім чынам, калі любы з сервераў праз які ідзе абмен вынікамі працы памрэ, то любое з кліенцкіх сховішчаў можа быць зкапіявана на сервер каб аднавіць усю інфармацыю. Кожнае сховішча на кожным з працоўных месцаў насамрэч поўная рэзервовая копія ўсіх дадзеных (гл. Малюнак 1-3).

Insert 18333fig0103.png 
Малюнак 1-3. Схема размеркаванага кантролю версій.

Апроч таго, шмат якія з гэтых сістэм выдатна працуюць з некалькімі аддаленымі сховішчамі, так што вы можаце адначасова па-рознаму узаемадзейнічаць з некалькімі рознымі групамі людзей у межах аднаго праекта. Гэта дазваляе наладжваць розные тыпы паслядоўнасцяў дзеянняў, што немагчыма з цэнтралізаванымі сістэмамі, такімі як іерархічныя мадэлі.

## Кароткая гісторыя Git ##

Як і шмат іншых вялікіх рэчаў у жыцці, Git пачынаўся са стваральнага разбурэння і палымяных спрэчак. Ядро Linux — праграмны праект з адкрытымі зыходнікамі даволі вялікага аб'ёму. На пряцягу большай часткі перыяду існавання ядра Linux змены ў ім распаўсюджваліся у выглядзе патчаў і архіваваных файлаў. У 2002 годзе праект распрацоўкі ядра Linux пачаў карыстацца BitKeeper — прапрыетарнай РСКВ.

У 2005 годзе адносіны паміж суполкай распрацоўшчыкаў ядра Linux і камерцыйнай кампаніяй, што распрацоўвала BitKeeper сапсаваліся і бясплатна карыстацца гэтай утылітай стала немагчыма. Гэта запатрабавала ад суполкі распрацоўшчыкаў Linux (і, ў прыватнасці, Лінуса Торвальдса (Linus Torvalds)), стваральніка Linux'а) стварыць іх уласную сістэму, заснаваную на некаторых з урокаў, якія яны вынеслі для сябе з досведу карыстання BitKeeper. Некаторыя з мэтаў новай сітэмы ніжэй:

*	Хуткасць
*	Просты дызайн
*	Моцная падтрымка нелінейнай распрацоўкі (сотні паралельных галін)
*	Цалкам размеркаваная
*	Магчымасць эфектыўна працаваць з вялікімі праектамі, кшталту ядра Linux (хуткасць і памер дадзеных)

З часу свайго з'яўлення ў 2005 годзе Git развіваўся і сталеў каб быць лёгкім у выкарыстанні і пры гэтым захоўваць гэтыя першапачатковыя якасці. Ён неверагодна хуткі, вельмі эфектыўны ў працы з вялікімі праектамі і мае неверагодную сістэму кіравання галінамі для нелінейных праектаў (гл. главу 3).

## Асновы Git ##

Такім чынам, што ж такое Git, калі ў двух словах? Гета вельмі важны для засваення раздзел, таму што калі вы зразумееце што такое Git і фундаментальныя асновы таго як ён працуе, то  эфектыўнае выкарыстанне Git можа стаць значна больш простым для вас. Пад час вывучэння Git пастарайцеся не абапірацца на ўспаміны пра іншыя СКВ, кшталту Subversion і Perforce, гэта дапаможа пазбегнуць памылак і разгубленасці пад час выкарыстання гэтай прылады. Git захоўвае інфармацыю і успрымае яе вельмі непадобна на іншыя сістэмы, нават не гледзячы на даволі блізкае падабенства карыстальніцкага інтэрфейсу. Разуменне гэтых адрозненняў дапаможа прадухіліць памылкі і разгубленасць пад час работы з Git.

### Здымкі, а не адрозненні ###

Асноўнае адрозненне Git ад любой іншай СКВ (уключаючы Subversion і кампанію) — тое як Git ўяўляе сабе дадзеныя, якіе захоўвае. Канцэптуальна, большасць іншых сістэмы захоўвае інфармацыю ў выглядзе набор змяненнеў. Гэтыя сістэмы (CVS, Subversion, Perforce, Bazaar і гэтай далей) ставяцца да інфармацыі, якую яны захозваюць, як да набора адрозненняў для кожнага з файлаў у параўнанні з папярэднім станам, як гэта паказана на Малюнку 1-4.

Insert 18333fig0104.png 
Малюнак 1-4. Іншыя сістэмы звычайна захоўваюць дадзеныя ў выглядзе набора зменаў для базавай версіі кожнага файла.

Git ўспрымае данныя ў сховішчы інакш. Замест таго, каб успрымаць іх як наборы зменаў, Git ставіцца да дадзеных хутчэй як да набора здымкаў стану невялікай файлавай стэмы. Кожны раз, калі вы захоўваеце дадзеныя вашага праекду ў Git, ён па-сутнасці, робіць здымак таго, як вашыя файлы выглядаюць ў гэты момант і спасылку на гэты здымак. Для павышэння эфектыўнасці, калі файл не змяняўся, то Git не захоўвае яго яшчэ раз, а проста робіць спасылку на яго папярэдні стан, які ўжо быў захаваны. Гіт успрымае дадзеныя больш падобна на тое, што паказана на Малюнку 1-5.

Insert 18333fig0105.png 
Малюнак 1-5. Git захоўвае дадзеныя як здымкі стану праекта пэўнага часу.

Гэта вельмі сур'ёзна адрознівае Git ад практычна ўсіх іншых СКВ. Гэта вымушае Git пераглядзець амаль усе аспекты кіравання версіямі, што большасць іншых сістэм узялі з сістэм папярэдняга пакалення. Гэта робіць Git больш падобным на невялікую файлавую сістэму з неверагодна магутнымі інструмантамі, створанымі каб працаваць паверх яе, чымсці на звычайную СКВ. Некаторыя з пераваг, які дае такі падыход да захоўвання дадзеных, мы разгледзім ў Раздзеле 3, пад час вывучэння працы з галінамі.

### Практычна ўсе аперацыі выконваюцца лакальна ###

Большасць аперацый у Git патрабуюць для працы толькі лакальныя файлы і рэсурсы, бо звычайна інфармацыя з іншых кампутараў у сетцы не патрэбныя. Калі вы карысталіся ЦСКВ, дзе большасць аперацый маюць дадатковыя затрымкі, звязаныя з працай праз сець, то гэты аспект Git прымусіць думаць, што богі хуткасці блаславілі гэтую сістэмы неверагоднымі здольнасцямі. Большасць аперацыі выглядае практычна імгненнымі, паколькі ўся гісторыя праекта захоўваецца непасрэдна на вашым лакальным дыску.

Напрыклад, каб паглядзець гісторыю праекта Git не трэба звяртацца да сервера, каб атрымаць гісторыю і адлюстраваць яе для вас — можна проста прачытаць яе непасрэдна з вашай лакальнай базы дадзеных. Гэта значыць, што вы убачыце гісторыю праекта практычна імгненна. Калі вы захацелі ўбачыць розніцу паміж бягучай версіяй файла і той, што была месяц таму, Git можа праглядзець файл месячнай даўніны і вылічыць розніцу паміж версіямі лакальна, замест таго каб прасіць у сервера зрабіць гэта, альбо выцягваць старую версію з сервера і потым зноўку ж вылічваць розніцу лакальна.

Да таго ж, гэта значыць што вельмі няшмат чаго нельга зрабіць калі вы па-за сеткай ці VPN. Калі вы ў самалёце ці ў цягніку і хочаце крыху папрацаваць, то вы можаце захоўваць праект ў СКВ (ці рабіць каміты, як яшчэ кажуць) без аніякіх праблем і перашкод ажно пакуль не з'явіцца сетка, з дапамогай якой вы зможаце выгрузіць змены. Калі вы прыйшлі дадому не і здолелі наладзіць VPN, вы ўсё яшчэ ў стане працаваць. У многіх іншых сістэмах вельмі цяжка, калі наогул магчыма рабіць так. У Perforce, напрыклад, вы няшмат што можаце зрабіць, калі няма сувязі з серверам, а ў Subversion і CVS вы можаце рэдактаваць файлы, але не будзеце ў стане захаваць змены ў сваю базу дадзеных (паколькі сувязі з базай дадзеных няма). Можа гэта і не выглядае вялікім дасягненнем, але вы будзеце здзіўленыя, убачыўшы наколькі гэта можа змяніць справу.

### Git правярае цэласнасць ###

Усе дадзеныя ў Git праходзяць працэдуру стварэння кантрольнай характарыстыкі і затым да іх можна звярнуцца па гэтай кантрольнай характарыстыцы. Такім чынам, немагчыма змяціь змест якога-небудзь файла ці тэчкі без таго, каб Git заўважыў гэтыя змены. Гэты функцыянал убудаваны ў Git на самым нізкім ўзроўні і з'яўляецца неад'емнай часткай філасофіі сістэмы. Вы не можаце страціць інфармацыю ці пашкодзіць файл так, каб Git не быў ў стане выявіць гэта.

Механізм, які выкарыстоўвае Git для стварэння кантрольнай характарыстыкі называецца хэш-сумай па алгарытме SHA-1. Хэш-сума ўяўляе сабою шаснаццацірычную лічбу (якая складаецца з лічбаў 0–9 і літар a–f) даўжынёю 40 знакаў і вылічваецца ў Git на  падставе зместа файла ці структуры тэчак. Выглядае хэш-сума SHA-1 прыблізна такім чынам:

	24b9da6552252987aa493b52f8696cd6d3b00373

Гэтыя хэшы можна ўбачыць паўсюль ў Git, бо яны выкарыўстоўваюцца там вельмі часта. Фактычна, Git захоўвае ўсё ў сваёй базе дадзеных не па імёнах файлаў, а звяртаючыся па хэш-сумах змесціва дадзеных.

### Git ў асноўным толькі дадае дадзеныя ###

Пры выкананні нейкіх дзеянняў у Git практычна заўсёды дадаюцца дадзеныя ў базу дадзеных. Даволі цяжка прымусіць сістэму выдаліць дадзеныя так ці інакш, ці зрабіць нешта, што нельга адмяніць. Як і ў любой СКВ, вы можаце згубіць ці заблытацца ў зменах, якія вы яшчэ не занеслі ў сістэму, але пасля таго, як вы захавалі здымак стаў у Git, яго вельмі цяжка згубіць, асабліва калі вы рэгулярна выгружаеце сваю базу ў іншы рэпазітар.

Гэта робіць выкарыстанне Git прыемным, нават, радасным, бо ведаеш, што ёсць магчымасць эксперыментаваць без небяспеки сапсаваць ўсё пад час эксперыменту. Для больш глыбокага разумення як Git захоўвае свае дадзеныя і як можна узнавіць дадзеныя, якія здаюцца згубленымі назаўсёды чытайце Главу 9.

### Тры станы ###

Увага! Гэта галоўнае, што вам трэба запомніць пра Git, калі вы хочаце каб рэшта працэсу навучання прайшла гладка. Git мае тры галоўных станы, у якіх могуць знаходзіцца вашыя файлы: захаваныя (закамічаныя ад англ. commited), змененыя і абраныя (англ. staged). Захаваныя — тыя файлы, якія ўжо бяспечна захоўваюцца ў лакальнай базе дадзеных. Змененыя файлы былі зменены, але яшчэ не былі захаваныя ў базу. Абраныя — гэта змененыя файлы, якія былі пазначаныя для таго, захаваць іх у іх цяперашняй версіі пад час наступнага каміту (сеанса захавання файлаў).
Now, pay attention. This is the main thing to remember about Git if you want the rest of your learning process to go smoothly. Git has three main states that your files can reside in: committed, modified, and staged. Committed means that the data is safely stored in your local database. Modified means that you have changed the file but have not committed it to your database yet. Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

Гэта падводзіць нас да трох галоўных секцый праекта ў Git: тэчкі Git ці рэпазітару (git directory на малюнку), працоўнай тэчкі (git directory на малюнку) і зоны ўвання (staging area).
This leads us to the three main sections of a Git project: the Git directory, the working directory, and the staging area.

Insert 18333fig0106.png 
Малюнак 1-6. Працоўная тэчка, зона файлаў, падрыхтаваных да захоўвання і тэчка Git.
Figure 1-6. Working directory, staging area, and git directory.

Тэчка Git гэта месца, дзе сістэма захоўвае метададзеныя і базу дадзеных з аб'ектамі вашага праекту. Гэта найбольш важная частка Git і менавіта яе копія робіцца, калі вы клануеце рэпазітар з іншага кампутара.
The Git directory is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from another computer.

Працоўная тэчка гэта фактычна стан пэўнай версіі праекту. Гэтыя файлы узятыя са сціснутай базы дадзеных у тэчцы Git і змешчаныя на дыску каб вы маглі імі карыстацца і мадыфікаваць.
The working directory is a single checkout of one version of the project. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.

Зона абраных файлаў гэта звычыйны файл, звычайна змешчаны ў тэчцы Git, які захоўвае інфармацыю пра ўсё, што было абрана і пойдзе у наступны каміт. Часам яго яшчэ называюць індэксам (index), але робіцца стандартам называць гэты файл зонай абраных файлаў (staging area).
The staging area is a simple file, generally contained in your Git directory, that stores information about what will go into your next commit. It’s sometimes referred to as the index, but it’s becoming standard to refer to it as the staging area.

Звычайна працэс працы з Git выглядае наступным чынам:
The basic Git workflow goes something like this:

1.	Вы змяняеце файлы ў сваёй працоўнай тэчцы.
1.	You modify files in your working directory.
2.	Падрыхтоўваеце файлы да захоўвання ў базе, дадаючы іх адбітак ў зону абраных файлаў.
2.	You stage the files, adding snapshots of them to your staging area.
3.	Захоўваеце файлы, у тым выглядзе, як яны былі змешчаныў у зону абраных файлаў, змяшчаючы іх ў тэчку Git.
3.	You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your Git directory.

Калі гэтая версія файла была захаваныя ў тэчцы git, то яна лічыцца захаванай (ці закамічанай). Калі была змененая, але пасля гэтага была дададзеная абраная для захоўвання, то яна лічыцца абранай (staged). І калі яна была змененая, але не была абраная для захоўвання, то гэта змененая версія файла. У Главе 2 вы даведаецеся больш пра гэтыя станы, і пра тое, як, альбо скарыстацца з кожнага з іх, альбо наогул прапусціць этап абраных файлаў.
If a particular version of a file is in the git directory, it’s considered committed. If it’s modified but has been added to the staging area, it is staged. And if it was changed since it was checked out but has not been staged, it is modified. In Chapter 2, you’ll learn more about these states and how you can either take advantage of them or skip the staged part entirely.

## Усталёўка Git ##
## Installing Git ##

Цяпер мы пачнем непасрэдна выкарыстоўваць Git. Пачнем ад пачатку — з усталёўкі. Ёсць некалькі метадаў выканаць усталёўку. Два асноўных, гэта ўсталёўка з зыходнікаў і усталёўка з гатовага пакету для вашае платформы.
Let’s get into using some Git. First things first—you have to install it. You can get it a number of ways; the two major ones are to install it from source or to install an existing package for your platform.

### Усталёўка з зыходнікаў ###
### Installing from Source ###

Калі гэта магчыма, усталёўка з зыходнікаў можа быць даволі карыснай, таму што вы атрымліваеце самую свежую версію. З кожнай новай версіяй распрацоўшчыкі Git імкнуцца дадаць як мага больш зручных паляпшэнняў інтэрфейсу, так што — калі вы нармальна ставіцеся да кампіляцыі праграм з зыходнікаў — лепш за ўсё атрымаць апошнюю версію. Часта дыстрыбутывы Linux змяшчаюць даволі старыя версіі пакетаў. Так што, калі вы не карыстаецеся вельмі новым дыстрыбутывам, ці, наадварот вельмі старым (backports), то зборка з зыходнікаў можа быць найлепшым выйсцем для вас.
If you can, it’s generally useful to install Git from source, because you’ll get the most recent version. Each version of Git tends to include useful UI enhancements, so getting the latest version is often the best route if you feel comfortable compiling software from source. It is also the case that many Linux distributions contain very old packages; so unless you’re on a very up-to-date distro or are using backports, installing from source may be the best bet.

Каб праінсталяваць Git, вы павінны мець наступныя бібліятэкі, ад якіх Git залежыць: curl, zlib, openssl, expat і libiconv. Напрыклад, калі вы карыстаецеся сістэмай, якая выкарыстоўвае yum (як, напрыклад, Fedora) ці apt-get (як сістэмы, пабудаваныя на Debian), то можна скарыстацца адной з наступных каманд, каб усталяваць ўсе патрэбныя пакеты:
To install Git, you need to have the following libraries that Git depends on: curl, zlib, openssl, expat, and libiconv. For example, if you’re on a system that has yum (such as Fedora) or apt-get (such as a Debian based system), you can use one of these commands to install all of the dependencies:

	$ yum install curl-devel expat-devel gettext-devel \
	  openssl-devel zlib-devel

	$ apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \
	  libz-dev libssl-dev

Калі усе залежнасці развязаныя, трэба зцягнуць апошні здымак з вэб-сайту Git:
When you have all the necessary dependencies, you can go ahead and grab the latest snapshot from the Git web site:

	http://git-scm.com/download
	
Затым зкампіляваць і ўсталяваць:
Then, compile and install:

	$ tar -zxf git-1.6.0.5.tar.gz
	$ cd git-1.6.0.5
	$ make prefix=/usr/local all
	$ sudo make prefix=/usr/local install

Калі ўсё скончана, вы можаце атрымаць Git праз сам Git для абнаўлення:
After this is done, you can also get Git via Git itself for updates:

	$ git clone git://git.kernel.org/pub/scm/git/git.git
	
### Усталёўка пад Linux ###
### Installing on Linux ###

Калі вы хочаце праінсталяваць Git з бінарнага ўсталявальніка, можна скарыстацца звычайнай прыладай для кіравання пакетамі, якая ідзе ў складзе вашага дыстрыбутыва. Калі вы ў Fedora, то можна скарыстацца yum:
If you want to install Git on Linux via a binary installer, you can generally do so through the basic package-management tool that comes with your distribution. If you’re on Fedora, you can use yum:

	$ yum install git-core

Ці калі вы ў заснаваным на Debian дыстрыбутыве, кшталту Ubuntu, скарыстайцеся apt-get:
Or if you’re on a Debian-based distribution like Ubuntu, try apt-get:

	$ apt-get install git-core

### Усталёка на Mac ###
### Installing on Mac ###

Існуе два лёхкіх спосаба ўсталяваць Git на Mac. Найпрасцейшы — скарыстацца графічным ўсталявальнікам, які можна загрузіць са старонкі Google Code (гл. Малюнак 1-7)
There are two easy ways to install Git on a Mac. The easiest is to use the graphical Git installer, which you can download from the Google Code page (see Figure 1-7):

	http://code.google.com/p/git-osx-installer

Insert 18333fig0107.png 
Малюнак 1-7. Усталявальнік Git для OS X.
Figure 1-7. Git OS X installer.

Іншы асноўны спосаб — усталяваць Git праз MacPorts (`http://www.macports.org`). Калі вы маеце праінсталяваны MacPorts, істалюйце Git з дапамогай
The other major way is to install Git via MacPorts (`http://www.macports.org`). If you have MacPorts installed, install Git via

	$ sudo port install git-core +svn +doc +bash_completion +gitweb

Не абавязкова дадаваць усе дадаткі, але вы можаце ўключыць +svn на выпадак, калі вам спатрэбіцца выкарыстоўваць Git з рэпазіторыямі Subversion (гл. Главу 8).
You don’t have to add all the extras, but you’ll probably want to include +svn in case you ever have to use Git with Subversion repositories (see Chapter 8).

### Усталёўка пад Windows ###
### Installing on Windows ###

Усталяваць Git пад Windows вельмі проста. Праект msysGit мае вельмі простую працэдуру усталёўкі. Дастаткова загрузіць усталявальнік ў выглядзе файла  exe са старонкі Google Code і запусціць яго:
Installing Git on Windows is very easy. The msysGit project has one of the easier installation procedures. Simply download the installer exe file from the Google Code page, and run it:

	http://code.google.com/p/msysgit

Пасля ўсталёўкі вы будзеце мець як версію для каманднага радка (уключаючы кліента SSH, які будзе вельмі карысны пазней), так і стандарную версію з графічным інтэрфейсам.
After it’s installed, you have both a command-line version (including an SSH client that will come in handy later) and the standard GUI.

## Пачатковая наладка Git ##
## First-Time Git Setup ##

Цяпер, калі вы маеце ўсталяваны Git, трэба зрабіць некалькі рэчаў, каб наладзіць вашае асяроддзе Git. Гэтыя рэчы трэба рабіць толькі аднойчы, пасля абнаўлення гэтыя наладкі не будуць знішчаныя. Канешне, вы можаце змяніць іх ў любы час, выканаўшы гэтыя каманды яшчэ раз.
Now that you have Git on your system, you’ll want to do a few things to customize your Git environment. You should have to do these things only once; they’ll stick around between upgrades. You can also change them at any time by running through the commands again.

Git мае прыладу пад назвай git config, якая дазваляе наладзіць зменныя, якія кіруюць ўсемі аспектамі таго, як Git выглядае і працуе. Гэтыя зменныя могуць захоўвацца ў трох розных месцах:
Git comes with a tool called git config that lets you get and set configuration variables that control all aspects of how Git looks and operates. These variables can be stored in three different places:

*	Файл `/etc/gitconfig`: Утрымлівае зменныя для ўсіх карыстальнікаў у сістэме і іх рэпазітараў. Калі ўказаны параметр ` --system` для `git config`, то для чытання і запісу зменных будзе выкарыстоўвацца менавіта гэты файл. 
*	`/etc/gitconfig` file: Contains values for every user on the system and all their repositories. If you pass the option` --system` to `git config`, it reads and writes from this file specifically. 
*	Файл `~/.gitconfig`: Спецыфічны для вашага карыстальніка. Каб Git для чытання і запісу выкарыстоўваў менавіта гэты файл выкарыстоўваецца опцыя `--global`. 
*	`~/.gitconfig` file: Specific to your user. You can make Git read and write to this file specifically by passing the `--global` option. 
*	Файлы наладак ў тэчцы git (`.git/config`) любога рэпазітара, якім вы зараз карыстаецеся: Спецыфічныя для гэтага канкрэтнага рэпазітара. Кожны ўзровень перавызначае зменныя папярэдняга ўзроўню, так што зменныя з `.git/config` перавызначаюць зменныя з  `/etc/gitconfig`.
*	config file in the git directory (that is, `.git/config`) of whatever repository you’re currently using: Specific to that single repository. Each level overrides values in the previous level, so values in `.git/config` trump those in `/etc/gitconfig`.

У сістэмах з Windows Git шукае файл `.gitconfig` ў хатняй(`$HOME`) тэчцы карыстальніка (`C:\Documents and Settings\$USER` для большасці карыстальнікаў). Апроч таго, будзе шукаць яшчэ і файл наладак файл /etc/gitconfig, але ўжо па адносным шляху, лічачы за корань карнявую тэчку MSys, то бок тэчку, куды быў усталяваны Git на вашым кампутары.
On Windows systems, Git looks for the `.gitconfig` file in the `$HOME` directory (`C:\Documents and Settings\$USER` for most people). It also still looks for /etc/gitconfig, although it’s relative to the MSys root, which is wherever you decide to install Git on your Windows system when you run the installer.

### Дазеныя карыстальніка ###
### Your Identity ###

Першыя наладкі, якія трэба выканаць пасля ўсталёўкі Git, гэта заданне вашага імя карыстальніка і адраса электроннай пошты. Гэта важна, таму што кожны раз, захоўваючы нешта ў базе дадзеных Git будзе выкарыстоўваць гэтую інфармацыю,  то бок, яна будзе нязменна прысутнічаць ў кожным каміце, які вы будзеце ажыццяўляць:
The first thing you should do when you install Git is to set your user name and e-mail address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you pass around:

	$ git config --global user.name "John Doe"
	$ git config --global user.email johndoe@example.com

Зноўку ж, гэтая наладка робіцца толькі раз, калі скарыстацца опцыяй `--global`, таму што ў такім выпадку Git заўсёды будзе карыстацца гэтай інфармацыяй для ўсяго, што вы робіце ў гэтай сістэме. Калі яе дрэба замяніць на іншае імя ці электронны адрас для нейкага аднаго праекту, то можна запусціць тую ж каманду, знаходзячыся ў тэчцы гэтага праекта, але ўжо без опцыі `--global`.
Again, you need to do this only once if you pass the `--global` option, because then Git will always use that information for anything you do on that system. If you want to override this with a different name or e-mail address for specific projects, you can run the command without the `--global` option when you’re in that project.

### Ваш рэдактар ###
### Your Editor ###

Калі дадзеныя вашага карыстальніка зададзеныя, вы можаце наладзіць тэкставы рэдактар па-вызначэнню, які будзе выкарыстоўвацца ў Git, калі трэба набраць паведамленне. Па-мзоўчванню, Git выкарыстоўвае прадвызначаны ў сістэме рэдактар, якім звычайна з'яўляецца Vi ці Vim. Калі вы хочаце карыстацца іншым тэкставым рэдактарам, напрыклад Emacs, трэба зрабіць наступнае:
Now that your identity is set up, you can configure the default text editor that will be used when Git needs you to type in a message. By default, Git uses your system’s default editor, which is generally Vi or Vim. If you want to use a different text editor, such as Emacs, you can do the following:

	$ git config --global core.editor emacs
	
### Выбар diff-утыліты ###
### Your Diff Tool ###

Яшчэ адна карысная опцыя, якую вы, магчыма, захочаце наладзіць, гэта задане diff-утыліты для вырашэння канфліктаў пры зліянні (merge). Напрыклад, кали вы жадаеце выкарыстоўваць vimdiff:
Another useful option you may want to configure is the default diff tool to use to resolve merge conflicts. Say you want to use vimdiff:

	$ git config --global merge.tool vimdiff

Git умее працаваць з accepts kdiff3, tkdiff, meld, xxdiff, emerge, vimdiff, gvimdiff, ecmerge і opendiff. Апроч гэтага, вы можаце наладзіць сваю уласную прыладу, як апісана ў Главе 7.
Git accepts kdiff3, tkdiff, meld, xxdiff, emerge, vimdiff, gvimdiff, ecmerge, and opendiff as valid merge tools. You can also set up a custom tool; see Chapter 7 for more information about doing that.

### Праверка наладак ###
### Checking Your Settings ###

Каб праверыць наладкі, можна скарыстацца камандай `git config --list`, каб вывесці спісак наладак, якія Git можа тут адшукаць:
If you want to check your settings, you can use the `git config --list` command to list all the settings Git can find at that point:

	$ git config --list
	user.name=Scott Chacon
	user.email=schacon@gmail.com
	color.status=auto
	color.branch=auto
	color.interactive=auto
	color.diff=auto
	...

Вы можаце убачыць нейкія параметры больш чым аднойчы, таму што Git можа атрымаць яго з розных файлаў (`/etc/gitconfig` і `~/.gitconfig`, напрыклад). У гэтым выпадку Git выкарыстоўвае апошняе значэнне для гэтага асобнага параметра.
You may see keys more than once, because Git reads the same key from different files (`/etc/gitconfig` and `~/.gitconfig`, for example). In this case, Git uses the last value for each unique key it sees.

Апроч таго, вы можаце праверыць значэнне толькі аднаго параметра з дапамогай каманды выгляду `git config {параметр}`:
You can also check what Git thinks a specific key’s value is by typing `git config {key}`:

	$ git config user.name
	Scott Chacon

## Атрыманне дапамогі?даведкі ##
## Getting Help ##

Калі вам спатрэбілася дапамога пад час выкарыстання Git, то атрымаць яе магчыма, выклікаўшы старонку даведкі (manpage), адной з трох наступных каманд:
If you ever need help while using Git, there are three ways to get the manual page (manpage) help for any of the Git commands:

	$ git help <каманда>
	$ git <каманда> --help
	$ man git-<каманда>

Напрыклад, каб атрымаць даведку па камандзе config дастаткова выканаць:
For example, you can get the manpage help for the config command by running

	$ git help config

Гэта вельмі зручна, таму што даведкай можна скарыстацца дзе і калі заўгадна, нават па-за сецівам. 
Калі даведкі і гэтай кнігі недастаткова і вам патрэбная дапамога спецыялісты, то вы можаце пашукаць яне на каналах `#git` ці `#github` на IRC серверы Freenode  (irc.freenode.net). Гэтыя каналы пастаянна запоўненыя сотнямі асоб, якія вельмі шмат ведаюць пра Git і даволі часта гатовыя дапамагчы.
These commands are nice because you can access them anywhere, even offline.
If the manpages and this book aren’t enough and you need in-person help, you can try the `#git` or `#github` channel on the Freenode IRC server (irc.freenode.net). These channels are regularly filled with hundreds of people who are all very knowledgeable about Git and are often willing to help.

## Вынікі ##
## Summary ##

Цяпер вы павінны мець некаторае ўяўленне пра Git і яго адрозненні ад ЦСКВ, якія могуць быць вам карыснымі. Апроч таго, зараз вы павінны мець працуючую версію Git у сваёй сістэме, у якой зададзеныя вашыя персанальныя дадзеныя. Цяпер прыйшоў час перайсці да асноў працы з Git.
You should have a basic understanding of what Git is and how it’s different from the CVCS you may have been using. You should also now have a working version of Git on your system that’s set up with your personal identity. It’s now time to learn some Git basics.
