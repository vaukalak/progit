# Першыя крокі #

Гэтая глава распавядзе, як пачаць працу з Git. Спачатку мы растлумачым асновы інструмэнтаў кіраваньня вэрсіямі, затым разьбяромся, як атрымаць працоўны Git на сваёй сыстэме і, урэшце, як наладзіць яго так, каб зь ім можна было пачаць працаваць. Напрыканцы гэтае главы вы будзеце разумець для чаго наогул прызначаны Git, чаму ім варта карыстацца, і будзеце ўмець наладжваць яго.

## Пра кіраваньне вэрсіямі ##

Што такое кіраваньне вэрсіямі, і нашто яно патрэбнае? Кіраваньне вэрсіямі — гэта сыстэма, якая запісвае зьмены, што адбыліся з файлам ці наборам файлаў зь цягам часу, так, каб потым вы маглі бачыць патрэбныя старыя вэрсіі. У прыкладах гэтай кнігі мы будзем працаваць з зыходнымі кодамі праграм, але, насамрэч, вы можаце працаваць практычна зь любымі тыпамі файлаў, якія існуюць на вашым кампутары.

Калі вы графічны ці вэб-дызайнэр і маеце намер захоўваць кожную вэрсію малюнкаў ці слаёў (што вам больш патрэбна), то выкарыстаньне сыстэмы кіраваньня вэрсіямі (СКВ, Version Control System, VCS) — гэта вельмі разумны выбар. Гэта дазволіць вам вярнуць файлы да папярэдняга стану, вярнуць да папярэдняга стану увесь праект, параўнаць зьмены паміж рознымі станамі, убачыць хто апошнім зьмяняў нешта, што можа выклікаць праблемы, хто прапанаваў зьмены і калі, і шмат іншага. Выкарыстаньне СКВ у асноўным значыць, што калі вы сапсавалі нешта ці страцілі файлы, то гэта можна лёгка аднавіць. Як дадатак, гэта не запатрабуе вялікіх намаганьняў і выдаткаў з вашага боку.

### Лякальныя сыстэмы кіраваньня вэрсіямі ###

Шмат людзей у якасьці мэтаду кіраваньня вэрсіямі выбіраюць капіяваньне файлаў у іншую тэчку (магчыма, з датай у назьве, калі чалавек досыць разумны). Гэты падыход вельмі распаўсюджаны з-за сваёй прастаты, але ён пакідае неверагодна шмат магчымасьцяў для памылак. Вельмі лёгка забыцца ў якой тэчцы вы цяпер знаходзіцеся й выпадкова запісаць ня ў той файл, ці скапіяваць зусім не туды, куды вы зьбіраліся.

Каб вырашыць гэтую праблему праграмісты шмат часу таму распрацавалі лякальныя СКВ, якія выкарыстоўваюць простую базу зьвестак каб захоўваць усе зьмены ў файлах, вэрсіі якіх адсочваюцца (гл. Малюнак 1-1).

Insert 18333fig0101.png 
Малюнак 1-1. Схема лякальнага кіраваньня вэрсіямі.

Адной з усевядомых у той час СКВ была rcs, якая ўсё яшчэ пастаўляецца зь вялікай колькасьцю кампутараў. Нават папулярная апэрацыйная сыстэма Mac OS X усталёўвае rcs у складзе пакунка Developer Tools. Праца гэтага дастасаваньня заснаваная на захаваньні на дыску ў адмысловым фармаце набораў латак (patch) (гэта запісы розьніцы паміж дзьвюма файламі) для кожнай зьмены файла. Гэта дапамагае вярнуць файл да любога з зафіксаваных станаў, пасьлядоўна накладаючы латкі адну за адной.

### Цэнтралізаваныя сыстэмы кіраваньня вэрсіямі ###

Наступнай вялікай праблемай, была неабходнасьць узаемадзейнічаць з распрацоўнікамі за іншымі кампутарамі. Цэнтралізаваныя сыстэмы кіраваньня вэрсіямі (ЦСКВ) былі распрацаваныя каб вырашыць гэтую праблему. Такія сыстэмы як CVS, Subversion і Perforce складаюцца з сэрвера, на якім захоўваюцца ўсе зьвесткі па вэрсіях файлаў, і некаторай колькасьці кліенцкіх машын, якія атрымліваюць файлы з сэрвера. Шмат год такая схема зьяўлялася стандартам кіраваньня вэрсіямі (гл. Малюнак 1-2).

Insert 18333fig0102.png 
Малюнак 1-2. Схема цэнтралізаванага кіраваньня вэрсіямі.

Гэты падыход мае шмат пераваг, асабліва ў параўнаньні зь лякальнымі СКВ. Напрыклад, усе дакладна ведаюць што астатнія робяць і што наогул адбываецца ў праекце. Адміністратары маюць зручную магчымасьць кантролю за тым, хто што можа зрабіць. І гэта значна прасьцей, чым адміністраваньне лякальных баз зьвестак СКВ на кожнай кліенцкай машыне.

Аднак, гэты падыход мае і некаторыя сур’ёзныя мінусы. Самы відавочны зь іх — цэнтральны сэрвер яўляе сабою пункт, крах якога цягне за сабою крах усёй сыстэмы. Калі гэты сэрвер спыніць працу на гадзіну — у гэтую гадзіну ніхто ня зможа абмяняцца з супрацоўнікамі вынікамі сваёй працы ці захаваць новую вэрсію таго, над чым ён ці яна зараз працуе. Калі жорсткі дыск, на якім зьмешчаная цэнтральная база зьвестак пашкодзіцца, а актуальных рэзэрвовых копіяў няма, то вы згубіце абсалютна ўсё: усю гісторыю праекту, за выключэньнем тых здымкаў, што карыстальнікі выпадкова мелі на сваіх лякальных кампутарах. Лякальныя СКВ пакутуюць на тую ж праблему: калі ты маеш усю гісторыю праекта толькі ў адным месцы, то ты рызыкуеш згубіць усё.

### Разьмеркаваныя сыстэмы кіраваньня вэрсіямі ###

І вось тут у гульню ўступаюць разьмеркаваныя сыстэмы кіраваньня вэрсіямі (РСКВ). У РСКВ (такіх як Git, Mercurial, Bazaar ці Darcs) кліенты ня толькі атрымліваюць апошнюю вэрсію файлаў: яны атрымліваюць поўную копію сховішча. Такім чынам, калі любы з сэрвераў праз які ідзе абмен вынікамі працы „памрэ“, то любое з кліенцкіх сховішчаў можа быць скапіявана на сэрвер, каб аднавіць усю інфармацыю. Кожнае сховішча на кожным з працоўных месцаў насамрэч поўная рэзэрвовая копія ўсіх зьвестак (гл. Малюнак 1-3).

Insert 18333fig0103.png 
Малюнак 1-3. Схема разьмеркаванай сыстэмы кіраваньня вэрсіямі.

Апроч таго, шмат якія з гэтых сыстэм выдатна працуюць зь некалькімі аддаленымі сховішчамі так, што вы можаце адначасова па-рознаму ўзаемадзейнічаць зь некалькімі рознымі групамі людзей у межах аднаго праекту. Гэта дазваляе наладжваць розныя тыпы пасьлядоўнасьцяў дзеяньняў, што немагчыма з цэнтралізаванымі сыстэмамі.

## Кароткая гісторыя Git ##

Як і шмат іншых вялікіх рэчаў у жыцьці, Git пачынаўся са стваральнага разбурэньня й палымяных спрэчак. Ядро Linux — праграмны праект з адкрытым зыходным кодам даволі вялікага аб’ёму. На працягу большай часткі пэрыяду існаваньня ядра Linux(1991–2002) зьмены ў ім распаўсюджваліся ў выглядзе латак і архіваў. У 2002 годзе праект распрацоўкі ядра Linux пачаў карыстацца BitKeeper — прапрыетарнай РСКВ.

У 2005 годзе адносіны паміж суполкай распрацоўнікаў ядра Linux і камэрцыйнай кампаніяй, што распрацоўвала BitKeeper, сапсаваліся, і бясплатна карыстацца гэтай утылітай стала немагчыма. Гэта запатрабавала ад суполкі распрацоўнікаў Linux (і, у прыватнасьці, Лінуса Торвальдса (Linus Torvalds), стваральніка Linux’а) стварыць іх уласную сыстэму, заснаваную на досьведзе, які яны атрымалі пад час карыстаньня BitKeeper. Некаторыя з патрабаваньняў да сыстэмы:

*	Хуткасьць
*	Просты дызайн
*	Моцная падтрымка нелінейнай распрацоўкі (сотні паралельных галін)
*	Цалкам разьмеркаваная
*	Магчымасьць эфэктыўна працаваць зь вялікімі праектамі, кшталту ядра Linux (хуткасьць і памер зьвестак)

З часу свайго зьяўленьня ў 2005 годзе Git разьвіваўся й сталеў каб быць лёгкім у выкарыстаньні і пры гэтым захоўваў гэтыя першапачатковыя якасьці. Ён неверагодна хуткі, вельмі эфэктыўны ў працы зь вялікімі праектамі і мае неверагодную сыстэму кіраваньня галінамі для нелінейных праектаў (гл. *Главу 3*).

## Асновы Git ##

Такім чынам, што ж такое Git у двух словах? Гэта вельмі важны для засваеньня разьдзел, таму што калі вы зразумееце, што такое Git і фундамэнтальныя асновы таго як ён працуе, то  эфэктыўнае выкарыстаньне Git можа стаць значна больш простым для вас. Пад час вывучэньня Git пастарайцеся не абапірацца на ўспаміны пра іншыя СКВ, кшталту Subversion і Perforce, гэта дапаможа пазьбегнуць памылак і разгубленасьці пад час выкарыстаньня гэтага інструмэнту. Git захоўвае інфармацыю і успрымае яе вельмі непадобна на іншыя сыстэмы, нават ня гледзячы на даволі блізкае падабенства карыстальніцкага інтэрфэйсу. Разуменьне гэтых адрозьненьняў дапаможа прадухіліць памылкі й разгубленасьць пад час работы з Git.

### Здымкі, а не адрозьненьні ###

Асноўнае адрозьненьне Git ад любой іншай СКВ (у тым ліку Subversion і кампанію) — тое як Git уяўляе сабе зьвесткі, якія захоўвае. Канцэптуальна, большасьць іншых сыстэм захоўвае інфармацыю ў выглядзе набору зьменаў. Гэтыя сыстэмы (CVS, Subversion, Perforce, Bazaar і гэтак далей) ставяцца да інфармацыі, якую яны захоўваюць, як да набору адрозьненьняў для кожнага з файлаў у параўнаньні з папярэднім станам, як гэта адлюстравана на Малюнку 1-4.

Insert 18333fig0104.png 
Малюнак 1-4. Іншыя сыстэмы звычайна захоўваюць зьвесткі ў выглядзе набору зьменаў для базавай вэрсіі кожнага файла.

Git успрымае зьвесткі ў сховішчы інакш. Замест таго, каб успрымаць іх як наборы зьменаў, Git ставіцца да зьвестак хутчэй як да набору здымкаў стану невялікай файлавай сыстэмы. Кожны раз, калі вы захоўваеце зьвесткі вашага праекту ў Git, ён па-сутнасьці, робіць здымак таго, як вашы файлы выглядаюць у гэты момант. Для павышэньня эфэктыўнасьці, калі файл не зьмяняўся, то Git не захоўвае яго яшчэ раз, а проста робіць спасылку на яго папярэдні стан, які ўжо быў захаваны. Git успрымае зьвесткі больш падобна на тое, што паказана на Малюнку 1-5.

Insert 18333fig0105.png 
Малюнак 1-5. Git захоўвае зьвесткі як здымкі стану праекта пэўнага часу.

Гэта вельмі сур’ёзна адрозьнівае Git ад практычна ўсіх іншых СКВ. Гэта ж вымушае Git пераглядзець амаль усе асьпекты кіраваньня вэрсіямі, што большасьць іншых сыстэм узялі з сыстэм папярэдняга пакаленьня. У выніку Git больш падобны на невялікую файлавую сыстэму зь неверагодна магутнымі інструмэнтамі, створанымі каб працаваць паверх яе, чымсьці на звычайную СКВ. Некаторыя зь пераваг, якія дае такі падыход да захаваньня зьвестак, мы разгледзім ў *Главе 3*, пад час вывучэньня працы з галінамі.

### Амаль усе апэрацыі выконваюцца лякальна ###

Большасьць апэрацый у Git патрабуюць для працы толькі лякальныя файлы й рэсурсы, бо звычайна інфармацыя зь іншых кампутараў у сетцы не патрэбная. Калі вы карысталіся ЦСКВ, дзе большасьць апэрацый маюць дадатковыя затрымкі, зьвязаныя з працай празь сеціва, то гэты асьпект Git прымусіць думаць, што богі надзялілі гэтую сыстэму неверагоднымі здольнасьцямі. Большасьць апэрацый выглядае практычна імгненнымі, паколькі ўся гісторыя праекту захоўваецца непасрэдна на вашым лякальным дыску.

Напрыклад, каб паглядзець гісторыю праекту Git ня трэба зьвяртацца да сэрверу, каб атрымаць гісторыю і адлюстраваць яе для вас, можна проста прачытаць яе непасрэдна з вашай лякальнай базы зьвестак. Гэта значыць, што вы ўбачыце гісторыю праекту практычна імгненна. Калі вы захацелі ўбачыць розьніцу паміж бягучай вэрсіяй файла і той, што была месяц таму, Git можа праглядзець файл месячнай даўніны й вылічыць розьніцу паміж вэрсіямі лякальна, замест таго, каб прасіць сэрвер зрабіць гэта, ці выцягнуць старую вэрсію з сэрвера й потым самастойна вылічваць розьніцу лякальна.

Да таго ж, гэта значыць што вельмі няшмат чаго нельга зрабіць, калі вы па-за сеткай ці VPN. Калі вы ў самалёце ці ў цягніку і хочаце крыху папрацаваць, то вы можаце захоўваць праект у СКВ (ці рабіць каміты, як яшчэ кажуць) без аніякіх праблем і перашкод, ажно пакуль не зьявіцца сетка, з дапамогай якой вы зможаце выгрузіць зьмены. Калі вы прыйшлі да дому й ня здолелі наладзіць VPN, вы ўсё роўна можаце працягваць працаваць. У шматлікіх іншых сыстэмах вельмі цяжка, калі наогул магчыма так зрабіць. У Perforce, напрыклад, вы няшмат што можаце зрабіць, калі няма сувязі з сэрверам, а ў Subversion і CVS вы можаце рэдагаваць файлы, але будзеце ня ў стане захаваць зьмены ў сваю базу зьвестак (паколькі сувязі зь ёю няма). Можа гэта й не выглядае вялікім дасягненьнем, але вы будзеце зьдзіўленыя, калі ўбачыце на колькі гэта можа зьмяніць справу.

### Git правярае цэласнасьць ###

Усе зьвесткі ў Git праходзяць працэдуру стварэньня кантрольнай сумы, і затым да іх можна зьвярнуцца па гэтай кантрольнай суме. Такім чынам, немагчыма зьмяніць зьмест якога-небудзь файла ці тэчкі без таго, каб Git не заўважыў гэтыя зьмены. Гэты функцыянал убудаваны ў Git на самым нізкім узроўні і зьяўляецца неад’емнай часткай філязофіі сыстэмы. Вы ня можаце страціць інфармацыю ці пашкодзіць файл так, каб Git ня быў у стане выявіць гэта.

Мэханізм, які выкарыстоўвае Git для стварэньня кантрольнай сумы называецца хэш-сумай па альгарытме SHA-1. Хэш-сума ўяўляе сабою шаснаццатковы лік (які складаецца зь лічбаў 0–9 і літар a–f) даўжынёю 40 знакаў і вылічваецца ў Git на падставе зьместу файла ці структуры тэчкі. Выглядае хэш-сума SHA-1 прыблізна такім чынам:

	24b9da6552252987aa493b52f8696cd6d3b00373

Гэтыя хэшы можна ўбачыць паўсюль у Git, бо яны выкарыстоўваюцца там вельмі часта. Фактычна, Git захоўвае ўсё ў сваёй базе зьвестак не па імёнах файлаў, а па хэш-сумах зьмесціва зьвестак.

### Git у асноўным толькі дадае зьвесткі ###

Пры выкананьні нейкіх дзеяньняў у Git практычна заўсёды дадаюцца зьвесткі ў базу. Даволі цяжка прымусіць сыстэму выдаліць зьвесткі так ці інакш, ці зрабіць нешта, што нельга адмяніць. Як і ў любой СКВ, вы можаце згубіць ці заблытацца ў зьменах, якія вы яшчэ не занесьлі ў сыстэму, але пасьля таго, як вы захавалі здымак стану у Git, яго вельмі цяжка згубіць, асабліва калі вы рэгулярна выгружаеце сваю базу ў іншае сховішча.

Гэта робіць выкарыстаньне Git прыемным, нават, радасным, бо ведаеш, што ёсьць магчымасьць экспэрымэнтаваць безь небясьпекі штосьці сапсаваць. Для больш глыбокага разуменьня як Git захоўвае свае зьвесткі і як можна ўзнавіць зьвесткі, якія здаюцца згубленымі назаўсёды чытайце *Главу 9*.

### Тры станы ###

Увага! Гэта галоўнае, што вам трэба запомніць пра Git, калі вы хочаце, каб далей навучаньне пайшло гладка. Git мае тры галоўныя станы, у якіх могуць знаходзіцца вашы файлы: *зафіксаваны (закамітаваны ад анг. commited)*, *мадыфікаваны* і *падрыхтаваны (анг. staged)*. Зафіксаваныя  файлы — тыя файлы, якія ўжо бясьпечна захоўваюцца ў лякальнай базе зьвестак. Мадыфікаваныя файлы былі зьменены, але яшчэ не захаваны ў базу. Падрыхтаваныя — гэта зьмененыя файлы, якія былі пазначаныя для захаваньня пад час наступнага камітаваньня (сэансу захаваньня файлаў).

Гэта падводзіць нас да трох галоўных сэкцыяў праекту ў Git: тэчкі Git (git directory на малюнку), працоўнай тэчкі (wokring directory) і прасторы рыхтаваньня (staging area).

Insert 18333fig0106.png 
Малюнак 1-6. Працоўная тэчка, прастора рыхтаваньня і тэчка Git.

Тэчка Git — гэта месца, дзе сыстэма захоўвае мэтазьвесткі й базу зьвестак з аб’ектамі вашага праекту. Гэта найбольш важная частка Git, і менавіта яе копія робіцца, калі вы клануеце сховішча зь іншага кампутара.

Працоўная тэчка гэта фактычна стан пэўнай вэрсіі праекту. Гэтыя файлы узятыя са сьціснутай базы зьвестак у тэчцы Git і зьмешчаныя на дыску, каб вы маглі імі карыстацца й мадыфікаваць.

Прастора рыхтаваньня гэта звычыйны файл, зьмешчаны ў тэчцы Git, які захоўвае інфармацыю пра ўсё, што было абрана й пойдзе ў наступны каміт. Часам яго яшчэ называюць *індэксам (index)*, але робіцца стандартам называць гэты файл *прасторай рыхтаваньня (staging area)*.

Звычайна працэс працы з Git выглядае наступным чынам:

1.	Вы зьмяняеце файлы ў сваёй працоўнай тэчцы.
2.	Рыхтуеце файлы да захаваньня ў базе — дадаеце іх адбітак у прастору рыхтаваньня.
3.	Робіце камітаваньне, паводле якога файлы зьмешчаныя ў прастору рыхтаваньня захоўваюцца ў тэчку Git.

Калі гэтая вэрсія файла была захаваная ў тэчцы Git, то яна лічыцца зафіксаванай (ці закамітаванай). Калі файл зьменены, але даданы ў прастору рыхтаваньня, то ён лічыцца падрыхтаваным (staged). І калі файл быў зьменены, але ня быў падрыхтаваным, то ён лічыцца мадыфікаваным. У *Главе 2* вы даведаецеся больш пра гэтыя станы, і пра тое, як альбо скарыстацца гэтым, альбо наагул прапусьціць этап рыхтаваньня файлаў.

## Усталяваньне Git ##

Цяпер мы пачнем непасрэдна выкарыстоўваць Git. Пачнем ад пачатку — з усталяваньня. Ёсьць некалькі мэтадаў, каб выканаць усталяваньне. Два асноўных — гэта усталяваньне з зыходнікаў і усталяваньне з гатовага пакунка для вашае плятформы.

### Усталяваньне з зыходнікаў ###

Калі гэта магчыма, усталяваньне з зыходнікаў можа быць даволі карысным, таму што вы атрымліваеце самую сьвежую вэрсію. З кожнай новай вэрсіяй распрацоўнікі Git імкнуцца дадаць як мага больш зручных паляпшэньняў інтэрфэйсу, так што, калі вы нармальна ставіцеся да кампіляцыі праграм з зыходнікаў, лепш за ўсё атрымаць апошнюю вэрсію. Часта дыстрыбутывы Linux зьмяшчаюць даволі старыя вэрсіі пакетаў. Таму, калі ваш дыстрыбутыў ня „першай сьвежасьці“, а можа й наагул вельмі стары, то зборка з зыходнікаў мае быць найлепшым выйсьцем.

Каб усталяваць Git, вы павінны мець наступныя бібліятэкі, ад якіх Git залежыць: curl, zlib, openssl, expat і libiconv. Калі вы карыстаецеся сыстэмай, якая выкарыстоўвае `yum` (як Fedora) ці `apt-get` (як сыстэмы, пабудаваныя на Debian), то можна скарыстацца адной з наступных камандаў, каб усталяваць усе патрэбныя пакеты:

	$ yum install curl-devel expat-devel gettext-devel \
	  openssl-devel zlib-devel

	$ apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \
	  libz-dev libssl-dev

Калі ўсе бібліятэкі ўсталяваныя, трэба запампаваць апошнюю вэрсію:

	http://git-scm.com/download

Затым скампіляваць і ўсталяваць:

	$ tar -zxf git-1.6.0.5.tar.gz
	$ cd git-1.6.0.5
	$ make prefix=/usr/local all
	$ sudo make prefix=/usr/local install

Калі ўсё скончана, вы можаце атрымаць Git праз сам Git для абнаўленьня:

	$ git clone git://git.kernel.org/pub/scm/git/git.git

### Усталваньне на Linux ###

Калі вы хочаце ўсталяваць Git зь бінарнага пакунка, можна скарыстацца звычайным дастасаваньнем для кіраваньня пакункамі, якое ідзе ў складзе вашага дыстрыбутыва. Калі вы ў Fedora, то можна скарыстацца `yum`:

	$ yum install git-core

Ці, калі вы ў заснаваным на Debian дыстрыбутыве кшталту Ubuntu, скарыстайцеся `apt-get`:

	$ apt-get install git-core	# у апошніх вэрсіях проста git

### Усталяваньне на Mac ###

Існуе два лёгкія спосабы ўсталяваць Git на Mac. Найпрасьцейшы — скарыстацца графічным ўсталявальнікам, які можна загрузіць са старонкі Google Code (гл. Малюнак 1-7):

	http://code.google.com/p/git-osx-installer

Insert 18333fig0107.png 
Малюнак 1-7. Усталявальнік Git для OS X.

Іншы распаўсюджаны спосаб — усталяваць Git праз MacPorts (`http://www.macports.org`). Калі вы маеце ўсталяваны MacPorts, усталюйце Git такім чынам:

	$ sudo port install git-core +svn +doc +bash_completion +gitweb

Не абавязкова ўсталёўваць усе дадаткі, але вы можаце ўключыць +svn на выпадак, калі вам спатрэбіцца выкарыстоўваць Git са сховішчам Subversion (гл. *Главу 8*).

### Усталяваньне на Windows ###

Усталяваць Git на Windows вельмі проста. Праект msysGit мае вельмі простую працэдуру ўсталяваньня. Дастаткова запампаваць усталявальнік у выглядзе файла  `exe` са старонкі Google Code і запусціць яго:

	http://code.google.com/p/msysgit

Пасьля ўсталяваньня вы будзеце мець як вэрсію для каманднага радка (разам з кліентам SSH, які будзе вельмі карысны пазьней), так і стандартную вэрсію з графічным інтэрфэйсам.

## Пачатковае наладжваньне Git ##

Цяпер, калі вы маеце ўсталяваны Git, трэба зрабіць некалькі рэчаў, каб наладзіць вашае асяродзьдзе Git. Гэтыя рэчы трэба рабіць толькі аднойчы, пасьля абнаўленьня гэтыя наладкі захаваюцца. Безумоўна, вы можаце зьмяніць іх у любы час, калі выканаеце гэтыя каманды яшчэ раз.

Git мае каманду пад назвай `git config`, якая дазваляе наладзіць парамэтры, якія кіруюць усімі аспэктамі таго, як Git выглядае і працуе. Гэтыя парамэтры могуць захоўвацца ў трох розных мейсцах:

*	Файл `/etc/gitconfig`: Утрымлівае парамэтры для ўсіх карыстальнікаў у сыстэме і іх сховішчаў. Калі вызначаны парамэтар `--system` для `git config`, то для чытаньня й запісу зьменных будзе выкарыстоўвацца менавіта гэты файл.
*	Файл `~/.gitconfig`: Спэцыфічны для вашага карыстальніка. Каб Git для чытаньня й запісу выкарыстоўваў менавіта гэты файл, пазначце опцыю `--global`. 
*	Файлы наладак у каталёгу git (`.git/config`) любога сховішча, якім вы зараз карыстаецеся: Спэцыфічныя для гэтага канкрэтнага сховішча. Кожны ўзровень перавызначае зьменныя папярэдняга ўзроўню, так што зьменныя з `.git/config` перавызначаюць зьменныя з  `/etc/gitconfig`.

У сыстэмах з Windows Git шукае файл `.gitconfig` у хатняй (`$HOME`) тэчцы карыстальніка (`C:\Documents and Settings\$USER` для большасьці карыстальнікаў). Апроч таго, Git будзе шукаць яшчэ і файл наладак `/etc/gitconfig`, але ўжо па адносным шляху MSys, то бок тэчку, куды быў усталяваны Git на вашым кампутары.

### Зьвесткі карыстальніка ###

Першыя наладкі, якія трэба выканаць пасьля ўсталяваньня Git, гэта заданьне вашага імя карыстальніка і адраса электроннай пошты. Гэта важна, таму што кожны раз, калі вы захоўваеце нешта ў базе зьвестак, Git будзе выкарыстоўваць гэтую інфармацыю. Такім чынам яна будзе нязьменна прысутнічаць у кожным каміце, які вы будзеце захоўваць:

	$ git config --global user.name "John Doe"
	$ git config --global user.email johndoe@example.com

Зноўку ж, гэтая наладка робіцца толькі раз, калі скарыстацца опцыяй `--global`, таму што ў такім выпадку Git заўсёды будзе карыстацца гэтай інфармацыяй для ўсяго, што вы робіце ў гэтай сыстэме. Калі яе трэба замяніць на іншае імя ці электронны адрас для нейкага аднаго праекту, то можна запусціць тую ж каманду, знаходзячыся ў тэчцы гэтага праекта, але ўжо без опцыі `--global`.

### Ваш рэдактар ###

Калі парамэтры вашага карыстальніка зададзеныя, вы можаце пазначыць тэкставы рэдактар, які будзе выкарыстоўвацца Git’ам пры неабходнасьці набраць паведамленьне. Першапачаткова Git выкарыстоўвае прадвызначаны ў сыстэме рэдактар, якім звычайна зьяўляецца Vi ці Vim. Калі вы хочаце карыстацца іншым тэкставым рэдактарам, напрыклад Emacs, трэба выканаць наступнае:

	$ git config --global core.editor emacs

### Выбар diff-утыліты ###

Яшчэ адна карысная опцыя, якую вы, магчыма, захочаце задаць, гэта diff-утыліта для вырашэньня канфліктаў пры *зьліцьці (merge)*. Напрыклад, калі вы жадаеце выкарыстоўваць vimdiff:

	$ git config --global merge.tool vimdiff

Git умее працаваць з kdiff3, tkdiff, meld, xxdiff, emerge, vimdiff, gvimdiff, ecmerge і opendiff. Апроч таго, вы можаце задаць сваё ўласнае дастасаваньне. Больш падрабязна напісана пра гэта ў *Главе 7*.

### Праверка наладак ###

Каб праверыць наладкі, можна скарыстацца камандай `git config --list`. Яна выводзіць сьпіс наладак, якія Git можа адшукаць:

	$ git config --list
	user.name=Scott Chacon
	user.email=schacon@gmail.com
	color.status=auto
	color.branch=auto
	color.interactive=auto
	color.diff=auto
	...

Вы можаце убачыць нейкія парамэтры больш за адзін раз, таму што Git можа атрымаць іх з розных файлаў (`/etc/gitconfig` і `~/.gitconfig`, напрыклад). У гэтым выпадку Git выкарыстоўвае апошняе значэньне для гэтага асобнага парамэтра.

Апроч таго, вы можаце праверыць значэньне толькі аднаго парамэтра з дапамогай каманды выгляду `git config {парамэтр}`:

	$ git config user.name
	Scott Chacon

## Атрыманьне дапамогі ##

Каб атрымаць дапамогу, калі яна вам спатрэбілася пад час выкарыстаньня Git, вы можаце выклікаць старонку даведкі адной з трох наступных камандаў:

	$ git help <каманда>
	$ git <каманда> --help
	$ man git-<каманда>

Напрыклад, каб атрымаць даведку па камандзе config дастаткова выканаць:

	$ git help config

Гэта вельмі зручна, таму што даведкай можна скарыстацца паўсюль, нават па-за сецівам.
Калі даведкі і гэтай кнігі недастаткова, і вам спатрэбіцца дапамога спэцыяліста, то вы можаце знайсьці яе на каналах `#git` і `#github` на IRC-сэрверы Freenode  (`irc.freenode.net`). Гэтыя каналы заўсёды запоўненыя сотнямі людзей, якія вельмі шмат ведаюць пра Git і даволі часта гатовыя дапамагчы.

## Вынікі ##

Цяпер вы маеце пэўнае ўяўленьне пра Git і яго карысныя адрозьненьні ад цэнтралізаваных СКВ. Апроч таго, вы ўжо павінны мець працоўную вэрсію Git у сваёй сыстэме з вашымі асабістымі зьвесткамі. Нарэшце прыйшоў час вывучыць некалькі базавых звычак работы з Git.
