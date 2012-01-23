# Падставы Git #

Калі вы жадаеце пачаць працаваць зь Git прачытаўшы толькі адну главу, то зараз вы чытаеце тое, што вам патрэбна. Гэтая глава зьмяшчае асноўныя каманды якія вам спатрэбяцца паводле працы зь Git. Напрыканцы, вы будзеце мець магчымасьць наладжваць і ініцыялізаваць сховішча, пачынаць і спыняць адсочваць файлы, рыхтаваць і захоўваць зьмены. Таксама мы растлумачым як ігнараваць некаторыя файлы, хутка выпраўляць памылкі, сачыць за гісторыяй вашага праекту, адлюстроўваць зьмены паміж камітамі і дадаваць і сьцягваць зьмены з аддаленага сховішча.

## Стварэньне сховішча Git ##

Існуе два падыходы стварэньня сховішча Git. Першы — гэта імпартаваць існы праект ці тэчку ў Git. Другі — кланаваць існае сховішча Git зь іншага сэрвэра.

### Ініцыялізацыя сховішча ў існай дырэкторыі ###

Каб пачаць адсочваць існы праект з дапамогай Git, вам спачатку неабходна перайсьці ў тэчку праекта і ўвесьці каманду:

	$ git init

Яна створыць новую паддырэкторыю `.git`, якая стрымлівае ўсе неабходныя файлы сховішча — шкілет сховішча Git. На дадзены момант яшчэ ніводны з файлаў праекту не адсочваецца. (Больш дакладную інфармацыю якія менавіта файлы захоўваюцца ў толькі што створанай дырэкторыі `.git` глядзіце ў *Главе 9*).

Калі вы жадаеце пачаць кантраляваць існыя файлы праекту (за выняткам пустых тэчак), вы мусіце праіндэксаваць іх і зафіксаваць першы каміт. Вы можаце зрабіць гэта некалькімі камандамі `git add`, якія праіндэксуюць неабходныя файлы, і затым `git commit`:

	$ git add *.c
	$ git add README
	$ git commit -m 'initial project version'

Мы разьбяром што робяць гэтыя каманды крыху пазьней. А зараз вы маеце сховішча Git з даданымі файламі і пачатковым камітам.

### Кланаваньне існага сховішча ###

Калі вы жадаеце атрымаць копію існага сховішча Git, напрыклад праекта, які вы хочаце падтрымаць, то вам спатрэбіцца каманда `git clone`. Калі вам вядомы іншыя сыстэмы кіраваньня вэрсіямі, напрыклад Subversion, то вы заўважыце, што каманда называецца `clone`, а не `checkout`. Гэта важлівае адрозьненьне — Git атрымлівае паўнавартасную копію даньняў з сэрвэра. Кожная вэрсія кожнага файлу сьцягваецца ў ваша сховішча, калі выконваецца каманда `git clone`. Фактычна, калі ваш сэрвэрны дыск зламаецца, то з дапамогай любога лякальнага сховішча любога кліента можна вярнуць сэрвэр у стан, ў якім быў зроблены клон дадзенага сховішча (вы, магчыма, згубіце частку сэрвэрных хукаў, але ўсе даньні, якія знаходзяцца пад вэрсійным кантролем, захаваюцца, падрабязьней гл. *Главу 4*).

Зклануйце сховішча загадам `git clone [url]`. Напрыклад, калі вы жадаеце атрымаць клон бібліятэкі Ruby Git - Grit, то зрабіце эта наступным чынам:

	$ git clone git://github.com/schacon/grit.git

Гэта створыць дырэкторыя `grit`, ініцыялізуе паддырэкторыю `.git`, сьцягне ўсе даньні і створыць працоўную копію праекта апошняй вэрсіі. Калі знойдзеце ў новую тэчку `grit`, вы пабачыце там файлы праекту зь якімі адразу можна працаваць. Калі жадаеце зрабіць клон у тэчке зь іншым імем, то трэба пазначыць яго ў загадным радку:

	$ git clone git://github.com/schacon/grit.git mygrit

Гэтая каманда зробіць тое што й папярэдняя, але ў тэчке `mygrit`.

Git можа працаваць зь некалькімі транспартнымі пратаколамі. Папярэдні прыклад выкарыстоўваў пратакол `git://`. Таксама вы можаце пабачыць пратакол `http(s)://` і `user@server:/path.git`, які карыстаецца SSH пратаколам. *Глава 4* распавядзе пра ўсе даступныя опцыі сэрвэра для доступу да вашага Git-сховішча і прааналізуе плюсы і мінусы кожнага.

## Запіс зьменаў у сховішча ##

Урэшце, вы маеце рэчаіснае Git сховішча і працоўную дырэкторыю з файламі праекту. Паводле працы вам будзе неабходна зьмяняць файлы і фіксаваць іх "здымкі" кожны раз, як праект будзе дасягаць патрэбнага вам стану.

Запамятайце, кожны файл у вашай працоўнай тэчке можа знаходзіцца ў адным з двух станаў: *адсочваемы (tracked)* і *неадсочваемы (untracked)*. Адсочваемыя файлы — гэта файлы, якія былі захаваныя ў апошнім "здымцы" праекту. Яны, у сваю чаргу, могуць быць *немадыфікаванымі*, *мадыфікаванымі* й *праіндэксаванымі*. *Неадсочваемыя* файлы — гэта ўсе астатнія файлы вашай працоўнай тэчкі. Іх няма ні ў апошніх "здымках" праекту, ні сярод праіндэксаваных файлаў. Калі вы першы раз клануеце сховішча, усе ягоныя файлы будуць адсочваемымі і немадыфікаванымі, бо вы толькі што зрабілі іх копію і не пасьпелі што-небудзь зьмяніць.

Як толькі вы адрэдагавалі файлы, Git пабачыць іх як мадыфікаваныя, таму што яны адрозьніваюцца ад файлаў у апошнім каміце. Вы мусіце *праіндэксаваць* гэтыя мадыфікаваныя файлы і затым закаміціць усе вашы праіндэксаваныя зьмены і гэтак далей, цыкл паўтараецца. Жыцьцёвы цыкл праілюстраваны на Дыяграме 2-1.

Insert 18333fig0201.png
Дыяграма 2-1. Жыцьцёвы цыкл стану вашых файлаў.

### Спраўджаньне стану вашых файлаў ###

Галоўным інструмэнтам, якім вы будзеце карыстацца для вызначэньня стану праекту, зьяўляецца каманда `git status`. Калі вы выканаеце гэтую каманду адразу пасьля кланаваньня праекту, то пабачыце прыкладна наступнае:

	$ git status
	# On branch master
	nothing to commit (working directory clean)

Гэта значыць, вы маеце чыстую працоўную дырэкторыю — іншымі словамі, вы ня маеце адсочваемых мадыфікаваных файлаў. Git таксама ня бачыць неадсочваемых файлаў, інакш яны былі б пералічаны тут. Нарэшце, каманда кажа ў якой галіне вы знаходзіцеся. Зараз гэта `master`, якая зьяўляецца прадвызначанай; цяпер гэта нязначна. Наступная глава распавядзе пра галіны і спасылкі больш падрабязна.

Давайце паглядзім што будзе, калі вы дадасьцё ў праект просты README файл. Калі гэты файл не існаваў да гэтага моманту, і вы выканаеце `git status`, вы ўбачыце ваш неадсочваемы файл:

	$ vim README
	$ git status
	# On branch master
	# Untracked files:
	#   (use "git add <file>..." to include in what will be committed)
	#
	#	README
	nothing added to commit but untracked files present (use "git add" to track)

Вы можаце пабачыць, што ваш новы README файл неадсочваецца, бо ён знаходзіцца пад загалоўкам “Untracked files” у вывадзе стану. Неадсочваемы азначае тое, што Git знайшоў файл, які адсутнічаў ў папярэднім "здымку" (каміце). Git ня будзе ўключаць яго ў ваш новы каміт, пакуль вы самі яму ня мовіце зрабіць гэта. Гэта абараняе вас ад дадаваньня ў праект аўтаматычна створаных файлаў і іншых, якія вы не жадаеце дадаваць. Калі вы сапраўды жадаеце дадаць гэты файл у праект, то ён мусіць стаць адсочваемым.

### Адсочваньне новых файлаў ###

Каб пачаць адсочваць файл, трэба скарыстацца камандай `git add`. Для вышэй узгаданага README файла выканайце:

	$ git add README

Калі вы запусьціце каманду статусу зноў, вы пабачыце ваш README файл у сьпісе адсочваемых і праіндэксаваных файлаў:

	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#	new file:   README
	#

Цяпер можна сказаць, што гэта праіндэксаваны файл, бо ён знаходзіцца пад загалоўкам “Changes to be committed”. Калі вы зробіце каміт у дадзены момант, вы захаваеце вэрсію файла, якая была ў момант выкананьня каманды `git add`. Як вы памятаеце, пасьля каманды `git init` вы запусьцілі `git add (files)` і тым самым пачалі адсочваць файлы ў дырэкторыі праекту. Каманда `git add` прымае шлях да файла ці тэчкі; калі зададзена тэчка, то каманда рэкурсыўна дадае ўсе ўнутраныя файлы.

### Індэксацыя мадыфікаваных файлаў ###

Давайце зьменім які-небудзь адсочваемы файл. Калі вы зьменіце раней дададзены файл `benchmarks.rb` і зноў выканаеце `git status`, вы атрымаеце нешта накшталт наступнага вываду:

	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#	new file:   README
	#
	# Changed but not updated:
	#   (use "git add <file>..." to update what will be committed)
	#
	#	modified:   benchmarks.rb
	#

Файл `benchmarks.rb` зьявіўся под загалоўкам “Changed but not updated”. Гэта значыць, што гэта мадыфікаваны адсочваемы файл, які не знаходзіцца ў прасторы індэксацыі. Каб праіндэксаваць яго, выканайце `git add` (гэта шматфункцыянальная каманда, якая выкарыстоўваецца для даданьня новых файлаў у праект, іх індэксацыі і для іншых мэтаў, напрыклад адзначэньне файлаў з вырашанымі канфліктамі аб'яднаньня). Давайце запусьцім `git add` для яго індэксацыі і паглядзім на вывад `git status`:

	$ git add benchmarks.rb
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#	new file:   README
	#	modified:   benchmarks.rb
	#

Абодва адлюстраваных файла праіндэксаваныя і будуць дададзеныя ў сховішча ў наступным каміце. Уявіце, што ў гэты момант вы ўспомнілі пра адну маленькую праўку якую вам патрэбна зрабіць перад тым як закаміціць зьмены. Вы адчыняеце файл, робіце і захоўваеце неабходныя праўкі і, здаецца, усё падрыхтавана для новага каміта. Але давайце яшчэ раз запусьцім `git status`:

	$ vim benchmarks.rb
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#	new file:   README
	#	modified:   benchmarks.rb
	#
	# Changed but not updated:
	#   (use "git add <file>..." to update what will be committed)
	#
	#	modified:   benchmarks.rb
	#

Якога д'ябла? Цяпер `benchmarks.rb` знаходзіцца і ў праіндэксаванай, і не ў праіндэксаванай прасторы. Як гэта магчыма? Гэта даказвае тое, што Git індэксуе файлы толькі тады, калі вы выконваеце `git add`. Калі ўжыць каміт зараз, то ў ім захаваецца вэрсія файла `benchmarks.rb`, якая была ў час апошняга запуску `git add`, а не `git commit`. Калі вы зьмянілі файл пасьля выкананьня каманды `git add`, то вы мусіце выканаць яе зноў, каб праіндэксаваць апошнюю вэрсію файла:

	$ git add benchmarks.rb
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#	new file:   README
	#	modified:   benchmarks.rb
	#

### Ігнараваньне файлаў ###

Часта, ваш праект будзе мець шэраг файлаў, якія вы ня толькі не захаціце аўтаматычна дадаваць у сховішча, але й бачыць іх сярод неадсочваемых. Гэта могуць быць аўтаматычна спароджаныя файлы, як log-файлы ці файлы створаныя вашай сыстэмай зборкі. У гэтым выпадку, вы можаце стварыць файл `.gitignore`, які будзе стрымліваць сьпіс шаблёнаў ігнаруемых файлаў у вашым праекце. Вось прыклад такога файла:

	$ cat .gitignore
	*.[oa]
	*~

Першы радок кажа Git'у ігнараваць усе файлы, якія сканчаюцца на `.o` ці `.a` — *аб'ектныя* і *архіўныя (бібліятэкі)* файлы, якія генэруюцца паводле зборкі вашага праекту. Другі радок кажа ігнараваць усе файлы, якія сканчаюцца на сымбаль `~`, які пазначае часовыя файлы, якія ствараюць мноства тэкставых рэдактараў кшталту Emacs. Вы таксама можаце ўключыць дырэкторыі `log`, `tmp` і `pid`, аўтаматычна ствараемую дакумэнтацыю і г.д. Дадаць файлы `.gitignore` у праект да пачатку асноўнай работы — вельмі добрая ідэя, бо такім чынам вы гарантуеце, што не закаміціце файлы, якія вы не жадаеце дадаваць у ваша Git сховішча.

Далей пералічаны правілы напісаньня шаблёнаў у файлах `.gitignore`:

*	Пустыя радкі й радкі, якія пачынаюцца з `#`, ігнаруюцца.
*	Можна выкарыстоўваць стандартныя glob шаблёны.
*	Можна завяршаць шаблён слэшам `/`, каб пазначыць дырэкторыю.
*	Можна інвэртаваць шаблён, калі прапісаць ў пачатку клічнік (`!`).

Glob шаблёны — гэта аналяг сталых выразаў, якія выкарыстоўваюць абалонкі. Зорачка (`*`) адпавядае любой колькасьці любых сымбаляў; `[abc]` — любому сымбалю, які знаходзіцца ў дужках (у дадзеным выпадку `a`, `b` ці `c`); пытальнік (`?`) — любому адзінаму сымбалю; дужкі, якія агароджваюць два сымбаля падзеленыя злучком (`[0-9]`), — любому сымбалю з гэтага дыяпазону.

Вось яшчэ некалькі прыкладаў радкоў з `.gitignore` файла:

	# камэнтар будзе праігнараваны
	*.a       # ігнараваць `.a`-файлы
	!lib.a    # за выняткам файла lib.a
	/TODO     # ігнараваць файл TODO толькі ў каранёвай тэчцы
	build/    # ігнараваць усе файлы ў дырэкторыі build/
	doc/*.txt # ігнараваць файлы кшталту doc/notes.txt, але ня doc/server/arch.txt

### Прагляд праіндэксаваных і непраіндэксаваных зьменаў ###

Калі загад `git status` вельмі недасканалы для вас, і вам неабходна ведаць якія менавіта зьмены адбыліся, а ня толькі ў якіх файлах яны адбыліся, то вы павінны скарыстацца камандай `git diff`. Больш падрабязна пра `git diff` мы распавядзём пазьней, а зараз хутчэй за ўсё вы будзеце выкарыстоўваць яе для атрыманьня адказу на два пытаньні: Што вы зьмянілі, але яшчэ не праіндэксавалі? і Што вы праіндэксавалі і зьбіраецеся зафіксаваць? Калі `git status` адказвае на гэтыя пытаньні вельмі абагульнена, то `git diff` адлюстроўвае вам паасобна кожны дададзены й выдалены радок — латку (patch), як яна ёсьць.

Уявім, вы зноў зьмянілі і праіндэксавалі файл `README`, а затым зьмянілі файл `benchmarks.rb`. Калі вы запусьціце `git status`, вы зноўку пабачыце нешта падобнае на гэта:

	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#	new file:   README
	#
	# Changed but not updated:
	#   (use "git add <file>..." to update what will be committed)
	#
	#	modified:   benchmarks.rb
	#

Каб убачыць што менавіта было зьменена і не праіндэксаванае, надрукуйце `git diff` без аргумэнтаў:

	$ git diff
	diff --git a/benchmarks.rb b/benchmarks.rb
	index 3cb747f..da65585 100644
	--- a/benchmarks.rb
	+++ b/benchmarks.rb
	@@ -36,6 +36,10 @@ def main
	           @commit.parents[0].parents[0].parents[0]
	         end

	+        run_code(x, 'commits 1') do
	+          git.commits.size
	+        end
	+
	         run_code(x, 'commits 2') do
	           log = git.commits('master', 15)
	           log.size

Гэтая каманда параўноўвае зьмест вашай працоўнай дырэкторыі зь зьместам прасторы індэксацыі. Вынік адлюстроўвае непраіндэксаваныя зьмены.

Калі вы жадаеце ўбачыць праіндэксаваныя зьмены, якія будуць дададзеныя ў наступным каміце, вы павінны выканаць `git diff --cached` (у Git 1.6.1 і вышэй вы можаце выканаць загад `git diff --staged`, які прасьцейшы для запамінаньня). Гэтая каманда параўноўвае праіндэксаваныя даньні і апошні каміт:

	$ git diff --cached
	diff --git a/README b/README
	new file mode 100644
	index 0000000..03902a1
	--- /dev/null
	+++ b/README2
	@@ -0,0 +1,5 @@
	+grit
	+ by Tom Preston-Werner, Chris Wanstrath
	+ http://github.com/mojombo/grit
	+
	+Grit is a Ruby library for extracting information from a Git repository

Заўважце, што `git diff` сам не адлюструе ўсіх зьменаў зробленых вамі пасьля апошняга каміту — толькі зьмены, якія застаюцца непраіндэксаванымі. Гэта можа заблытаць, бо калі вы ўсё праіндэксавалі, `git diff` нічога не пакажа ў вывадзе.

Іншы прыклад. Вы праіндэксавалі файл `benchmarks.rb` і потым адрэдагавалі яго. Вы можаце выканаць `git diff`, каб убачыць праіндэксаваныя зьмены і зьмены непраіндэксаваныя:

	$ git add benchmarks.rb
	$ echo '# test line' >> benchmarks.rb
	$ git status
	# On branch master
	#
	# Changes to be committed:
	#
	#	modified:   benchmarks.rb
	#
	# Changed but not updated:
	#
	#	modified:   benchmarks.rb
	#

Цяпер выканайце `git diff`, каб убачыць непраіндэксаваныя зьмены:

	$ git diff
	diff --git a/benchmarks.rb b/benchmarks.rb
	index e445e28..86b2f7c 100644
	--- a/benchmarks.rb
	+++ b/benchmarks.rb
	@@ -127,3 +127,4 @@ end
	 main()

	 ##pp Grit::GitRuby.cache_client.stats
	+# test line

і `git diff --cached` для праіндэксаваных:

	$ git diff --cached
	diff --git a/benchmarks.rb b/benchmarks.rb
	index 3cb747f..e445e28 100644
	--- a/benchmarks.rb
	+++ b/benchmarks.rb
	@@ -36,6 +36,10 @@ def main
	          @commit.parents[0].parents[0].parents[0]
	        end

	+        run_code(x, 'commits 1') do
	+          git.commits.size
	+        end
	+
	        run_code(x, 'commits 2') do
	          log = git.commits('master', 15)
	          log.size

### Фіксацыя зьменаў ###

Цяпер, калі ваша прастора індэксацыя ўсталяваная, вы можаце закаміціць вашы зьмены. Запомніце, усё што засталося непраіндэксаваным — любыя файлы, якія вы стварылі ці мадыфікавалі пасьля запуску `git add` — ня будуць уключаныя ў каміт. Яны застануцца пазначанымі як мадыфікаваныя файлы на вашым дыску.
У нашым выпадку, паводле апошняга запуску `git status`, вы бачылі што ўсе файлы былі праіндэксаваныя, таму вы падрыхтаваныя да прыманьня вашага каміту. Самы просты шлях зрабіць гэта — выканаць `git commit`:

	$ git commit

Дадзеная каманда запусьціць ваш тэкставы рэдактар (ён вызначаецца зьменнай асяродзьдзя `$EDITOR` — звычайна гэта vim ці emacs, але вы можаце ўсталяваць яго па свайму густу выкарыстаўшы каманду `git config --global core.editor`, як гэта апісана ў *Главе 1*).

Рэдактар адлюструе наступны тэкст (гэта прыклад зь Vim'а):

	# Please enter the commit message for your changes. Lines starting
	# with '#' will be ignored, and an empty message aborts the commit.
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#       new file:   README
	#       modified:   benchmarks.rb
	~
	~
	~
	".git/COMMIT_EDITMSG" 10L, 283C

Вы бачыце, што прадвызначана каміт утрымлівае закамэнтаваны вывад каманды `git status` і адзін пусты радок зьверху. Можна выдаліць гэты камэнтар і напісаць сваё паведамленьне, ці пакінуць яго для ўзгадваньня дзе былі зроблены зьмены. Для яшчэ большай інфармацыі пра зьмены, вы можаце дадаць опцыю `-v` каманддзе `git commit`. У выніку ў камэнтарах будзе прысутнічаць вывад каманды `git diff`, і вы будзеце дакладна ведаць што вы зрабілі. Калі вы пакінеце рэдактар, Git створыць каміт з вашым паведамленьнем (камэнтар будзе адсутнічаць).

Як варыянт, вы можаце надрукаваць ваша паведамленьне ў загадным радку каманды `commit` пасьля опцыі `-m`:

	$ git commit -m "Story 182: Fix benchmarks for speed"
	[master]: created 463dc4f: "Fix benchmarks for speed"
	 2 files changed, 3 insertions(+), 0 deletions(-)
	 create mode 100644 README

Вось цяпер вы стварылі свой першы каміт! Вывад каманды дае неабходную інфармацыю пра яго: галіну, ў якой ён захаваны (`master`); кантрольную суму SHA-1 (`463dc4f`); колькасьць зьмененых файлаў; статыстыку дадаваньня й выдаленьня радкоў.

Запомніце, што каміт запісвае здымак стану праекту, які вы захавалі ў прасторы індэксацыі. Усё што не было праіндэксавана так і застанецца ў мадыфікаваным стане. Вы можаце захаваць усё астатняе ў іншым каміце. Кожны раз, калі вы захоўваеце каміт, вы робіце здымак стану праекту, да якога вы зможаце вярнуцца пазьней, ці параўноўваць зь ім бягучы стан праекту.

### Мінаем прастору індэксацыі ###

Ня гледзячы на тое, што індэксацыя можа быць надзвычай карысна для стварэньня камітаў, але часам яна дадае больш складанасьцей у працэс распрацоўкі. Калі вы жадаеце абмінуць сыстэму індэксацыі, то Git прапануе вам просты спосаб зрабіць гэта. Дадаўшы опцыю `-a` да каманды `git commit`, вы загадваеце Git'у аўтаматычна праіндэксаваць усе адсочваемыя файлы й закаміціць іх. Давайце зробім каміт безь індэксацыі:

	$ git status
	# On branch master
	#
	# Changed but not updated:
	#
	#	modified:   benchmarks.rb
	#
	$ git commit -a -m 'added new benchmarks'
	[master 83e38c7] added new benchmarks
	 1 files changed, 5 insertions(+), 0 deletions(-)

Заўважце, што ў гэты раз вам не спатрэбілася запускаць `git add` для файла `benchmarks.rb` перад камітам.

### Выдаленьне файлаў ###

Каб выдаліць файл зь Git, вам неабходна выдаліць яго са сьпісу адсочваемых файлаў (дакладней, выдаліць яго з прасторы індэксацыі) і зрабіць каміт. Каманда `git rm` зробіць гэта і яшчэ выдаліць файл з вашай працоўнай тэчкі, і наступны раз вы яго ня ўбачыце як неадсочваемы.

Калі вы проста выдаліце файл з працоўнай тэчкі, то пасьля запуску `git status` вы ўбачыце яго ў разьдзеле “Changed but not updated (Зьмененыя, але не абноўленыя)” (то бок *непраіндэксаваным*):

	$ rm grit.gemspec
	$ git status
	# On branch master
	#
	# Changed but not updated:
	#   (use "git add/rm <file>..." to update what will be committed)
	#
	#       deleted:    grit.gemspec
	#

Далей, калі вы выканаеце `git rm`, Git праіндэксуе яго як выдаленага:

	$ git rm grit.gemspec
	rm 'grit.gemspec'
	$ git status
	# On branch master
	#
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#       deleted:    grit.gemspec
	#

Пасьля наступнага каміта, файл больш ня будзе адсочвацца. Калі вы ўжо зьмянілі файл і праіндэксавалі яго, то каб Git выдаліў яго, неабходна выканаць прымусовае выдаленьне з опцыяй `-f`. Гэта зроблена, каб прадухіліць выпадковае выдаленьне даньняў, якія былі зьмененыя і не захаваныя ў сховішчы.

Другая карысная рэч якую вы можаце захацець зрабіць — гэта выдаленьне файла з прасторы індэксацыі, але пакіданьне яго ў працоўнай дырэкторыі. Іншымі словамі, вы жадаеце пакінуць файл на вашым жорсткім дыску, але Git не павінен больш адсочваць яго. Гэта можа спатрэбіцца, калі вы забылі нешта прапісаць у `.gitignore` файл і выпадкова праіндэксавалі непатрэбны файл, як вялікі log-файл ці пакунак `.a`-файлаў. У такіх выпадках трэба скарыстацца опцыяй `--cached`:

	$ git rm --cached readme.txt

Для `git rm` вы можаце пазначыць файлы, дырэкторыі ці glob-шаблёны. То бок вы маеце магчымасьць прапісаць нешта кшталту:

	$ git rm log/\*.log

Зьвярніце ўвагу, што перад зорачкай `*` стаіць адваротны слэш `\`. Гэта неабходна, таму што Git выкарыстоўвае сваё пашырэньне для апрацоўкі шаблёнаў імён файлаў. Гэтая каманда выдаліць усе файлы, якія маюць пашырэньне `.log` у тэчцы `log/`. Ці вы можаце напісаць нешта наступнае:

	$ git rm \*~

Гэтая каманда выдаляе ўсе файлы, якія сканчваюцца на `~`.

### Перамяшчэньне файлаў ###

У адрозьненьні ад іншых сыстэм кіраваньня вэрсіямі, Git непасрэдна не падтрымлівае перамяшчэньне файлаў. Калі вы пераймянуеце файл, у Git'е не захавае аніякіх мэтаданьняў, пра тое, што вы яго перайменавалі. Аднак, Git дастаткова разумны, каб вызначыць ужо зьдзейсьнены факт перайменаваньня — перамяшчэньне файлаў мы разглядзім крыху пазьней.

Такім чынам, наяўнасьць каманды Git `mv` можа трохі заблытаць. Калі вы жадаеце перайменаваць файл у Git, вы мусіце выканаць наступнае:

	$ git mv file_from file_to

І гэта будзе выдатна працаваць. Калі вы сапраўды выканаеце гэта, і паглядзіце на стан сховішча, вы ўбачыце, што Git улічвае перайменаваньне файла:

	$ git mv README.txt README
	$ git status
	# On branch master
	# Your branch is ahead of 'origin/master' by 1 commit.
	#
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#       renamed:    README.txt -> README
	#

Аднак, гэта ўсё эквівалентна наступным дзеяньням:

	$ mv README.txt README
	$ git rm README.txt
	$ git add README

Git няяўна высьвятляе што было перайменавана, таму ня мае значэньня так ці з дапамогай каманды `mv` вы перайменавалі файл. Сапраўдная розьніца паміж гэтымі шляхамі, што `mv` — гэта каманда, якая замяняе тры — функцыя для зручнасьці. Больш важна тое, што вы можаце выкарыстоўваць любы спосаб перайменаваньня файлаў, і перад камітам выкарыстаць `add/rm`.

## Прагляд гісторыі камітаў ##

Пасьля таго як вы зрабілі некалькі камітаў, ці атрымалі клон сховішча з існай гісторыяй камітаў, вы магчыма захочаце ўбачыць што было зроблена ў праекце да гэтага часу. Самым асноўным і карысным інструмэнтам для гэтага зьяўляецца `git log`.

Наступныя прыклады выкарыстоўваюць вельмі просты праект, які называецца `simplegit`. Яго я часта выкарыстоўваю для дэманстрацыі. Каб атрымаць яго выканайце 

	git clone git://github.com/schacon/simplegit-progit.git

Калі ў гэтым прекце вы запусьціце `git log`, вывад будзе выглядаць прыкладна так:

	$ git log
	commit ca82a6dff817ec66f44342007202690a93763949
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Mon Mar 17 21:52:11 2008 -0700

	    changed the version number

	commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Sat Mar 15 16:40:33 2008 -0700

	    removed unnecessary test code

	commit a11bef06a3f659402fe7563abf99ad00de2209e6
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Sat Mar 15 10:31:28 2008 -0700

	    first commit

Прадвызначана, без аргумэнтаў, `git log` адлюстроўвае сьпіс зробленых камітаў у адваротным храналягічнаму парадку. То бок самыя апошнія каміты бачныя першымі. Як вы заўважылі, кожны каміт стрымлівае яго кантрольную суму SHA-1, імя і электронную пошту аўтара, дату захаваньня, і паведамленьне.

Вялікая колькасьць і разнастайнасьць опцыяў каманды `git log` дазваляе дакладна вызначаць вывад, які вы жадаеце ўбачыць. Зараз мы вам распавядзём пра некаторыя найбольш ужывальныя зь іх.

Адна з самых карысных опцыяў — гэта `-p`, якая паказвае diff-паведамленьне для кожнага каміта. Вы таксама можаце дадаць опцыю `-2`, якая абмяжуе вывад апошнімі дзьвюма камітамі:

	$ git log -p -2
	commit ca82a6dff817ec66f44342007202690a93763949
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Mon Mar 17 21:52:11 2008 -0700

	    changed the version number

	diff --git a/Rakefile b/Rakefile
	index a874b73..8f94139 100644
	--- a/Rakefile
	+++ b/Rakefile
	@@ -5,7 +5,7 @@ require 'rake/gempackagetask'
	 spec = Gem::Specification.new do |s|
	-    s.version   =   "0.1.0"
	+    s.version   =   "0.1.1"
	     s.author    =   "Scott Chacon"

	commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Sat Mar 15 16:40:33 2008 -0700

	    removed unnecessary test code

	diff --git a/lib/simplegit.rb b/lib/simplegit.rb
	index a0a60ae..47c6340 100644
	--- a/lib/simplegit.rb
	+++ b/lib/simplegit.rb
	@@ -18,8 +18,3 @@ class SimpleGit
	     end

	 end
	-
	-if $0 == __FILE__
	-  git = SimpleGit.new
	-  puts git.show
	-end
	\ No newline at end of file

Дадзеная опцыя адлюстроўвае тую ж інфармацыю, але разам з зробленымі зьменамі пад кожным элемэнтам сьпісу. Гэта вельмі зручны рэжым для агляду коду ці для неабходнасьці хутка зразумець, якія зьмены зрабіў ваш супрацоўнік.
Таксама разам зь `git log` вы можаце выкарыстоўваць опцыі з групы абагульняючых парамэтраў. Напрыклад, калі вы жадае ўбачыць кароткую статыстыку па кожнаму каміту, вы мусіце дадаць опцыю `--stat`:

	$ git log --stat
	commit ca82a6dff817ec66f44342007202690a93763949
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Mon Mar 17 21:52:11 2008 -0700

	    changed the version number

	 Rakefile |    2 +-
	 1 files changed, 1 insertions(+), 1 deletions(-)

	commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Sat Mar 15 16:40:33 2008 -0700

	    removed unnecessary test code

	 lib/simplegit.rb |    5 -----
	 1 files changed, 0 insertions(+), 5 deletions(-)

	commit a11bef06a3f659402fe7563abf99ad00de2209e6
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Sat Mar 15 10:31:28 2008 -0700

	    first commit

	 README           |    6 ++++++
	 Rakefile         |   23 +++++++++++++++++++++++
	 lib/simplegit.rb |   25 +++++++++++++++++++++++++
	 3 files changed, 54 insertions(+), 0 deletions(-)

Як вы бачыце, опцыя `--stat` друкуе пад кожным камітам сьпіс мадыфікаваных файлаў, іх колькасьці і колькасьць радкоў дадзеных і выдаленых. А ў канцы абагульняючая інфармацыя пра ўсе зьмены.
Другая сапраўды карысная опцыя — `--pretty`. Гэтая опцыя зьмяняе фармат вываду. Даступна некалькі перадусталяваных варыянтаў. `oneline` друкуе кожны каміт адным радком, што можа быць зручна, калі вы праглядаеце шмат камітаў. У дадатак да гэтага ёсьць опцыі `short`, `full` і `fuller`, якія, практычна не зьмяняючы фармат, выводзяць менш ці больш інфармацыі адпаведна:

	$ git log --pretty=oneline
	ca82a6dff817ec66f44342007202690a93763949 changed the version number
	085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 removed unnecessary test code
	a11bef06a3f659402fe7563abf99ad00de2209e6 first commit

Найбольш цікавая опцыя — `format`, якая дазваляе вызначаць фармат вываду журнала. Яна асабліва карысна, калі вам неабходна генэраваць вывад для далейшага машыннага разбору — вы можаце дакладна вызначыць фармат і быць упэўненымі, што ён ня зьменіцца пасьля абнаўленьня Git.

	$ git log --pretty=format:"%h - %an, %ar : %s"
	ca82a6d - Scott Chacon, 11 months ago : changed the version number
	085bb3b - Scott Chacon, 11 months ago : removed unnecessary test code
	a11bef0 - Scott Chacon, 11 months ago : first commit

Табліца 2-1 зьмяшчае сьпіс некалькіх найбольш ужываных опцый для ўсталяваньня фармату.

	Опцыя	Апісаньне вываду
	%H	Хэш каміту
	%h	Скарочаны хэш каміту
	%T	Хэш дрэва
	%t	Скарочаны хэш дрэва
	%P	Бацькоўскія хэшы
	%p	Скарочаныя бацькоўскія хэшы
	%an	Імя аўтара
	%ae	Электронная пошта аўтара
	%ad	Дата аўтара (фармат вызначаецца --date= )
	%ar	Дата аўтара, адносная
	%cn	Імя камітэра
	%ce	Электронная пошта камітэра
	%cd	Дата камітэра
	%cr	Дата камітэра, адносная
	%s	Паведамленьне

Вы верагодна зацікавіцеся ў чым розьніца паміж _аўтарам_ і _камітэрам_. _Аўтар_ — гэта асоба, якая напісала латку, а _камітэр_ — гэта той, хто ўжыў яе да праекту. Таму, калі вы адаслалі аднаму з распрацоўшчыкаў праекту сваю латку, то і яго, і ваша імя будзе ў каміце: яго — як камітэра, ваша — як аўтара. Больш падрабязна разглядзім гэта у *Главе 5*.

Опцыі `oneline` і `format` асабліва карысныя для іншай опцыі каманды `log` — `--graph`. Гэта опцыя просты ASCII-граф, які адлюстроўвае галіны і аб'яднаньні ў гісторыі. Яго вы можаце пабачыць у вашай копіі сховішча Grit:

	$ git log --pretty=format:"%h %s" --graph
	* 2d3acf9 ignore errors from SIGCHLD on trap
	*  5e3ee11 Merge branch 'master' of git://github.com/dustin/grit
	|\
	| * 420eac9 Added a method for getting the current branch.
	* | 30e367c timeout code and tests
	* | 5a09431 add timeout protection to grit
	* | e1193f8 support for heads with slashes in them
	|/
	* d6016bc require time for xmlschema
	*  11d191e Merge branch 'defunkt' into local

Мы разглядзелі толькі самыя простыя опцыі для фарміраваньня вываду `git log`, але іх значна больш. Табліца 2-2 зьмяшчае больш поўны іх сьпіс разам з апісаньнем іх узьдзеяньня на вывад.

	Опцыя	Апісаньне
	-p	Адлюстроўвае латку ўнесеную кожным камітам.
	--stat	Адлюстроўвае статыстыку мадыфікацыі файлаў кожнага каміту.
	--shortstat	Выводзіць толькі колькасьць зьмененых/даданых/выдаленых радкоў з опцыі --stat.
	--name-only	Адлюстроўвае сьпіс мадыфікаваных файлаў пасьля кожнага каміту.
	--name-status	Адлюстроўвае сьпіс файлаў разам зь інфармацыяй пра даданьне/мадыфікацыю/выдаленьне.
	--abbrev-commit	Адлюстроўвае толькі некалькі першых знакаў з кантрольнай сумы SHA-1 каміту (усе займаюць 40).
	--relative-date	Адлюстроўвае дату ў адносным фармаце (напрыклад, “2 тыдні назад”) замест паўнавартаснай формы.
	--graph	Адлюстроўвае ASCII-граф галін і аб'яднаньняў ў гісторыі праекту ў вывадзе.
	--pretty	Адлюстроўвае каміт у альтэрнатыўным фармаце. Аргумэнты — oneline, short, full, fuller і format (дзе вы маеце магчымасьць самастойна ўсталяваць патрэбны фармат).

### Абмежаваньне вываду гісторыі ###

Акрамя опцыяў для фарматаваньня вываду, `git log` мае шэраг карысных опцыяў для абмежаваньня вываду, яны дазваляюць адлюстраваць толькі пэўнае падмноства камітаў. Вы ўжо бачылі адну зь іх — гэта опцыя `-2`, якая адлюструе толькі два апошніх каміта. На самой справе, вы можаце пазначыць `-<n>`, дзе `n` — нейкі цэлы лік. На практыцы, вы наўрад ці будзеце часта выкарыстоўваць яе, бо Git прадвызначана прапускае ўвесь свой вывад праз пэйджэр (pager), таму вы бачыце толькі адну старонку вываду.

Аднак опцыя абмежаваньня паводле часу, такія як `--since` і `--until`, вельмі папулярныя. Напрыклад, наступная каманда атрымае сьпіс камітаў зроблены ў апошнія два тыдні:

	$ git log --since=2.weeks

Яна разумее мноства фарматаў — вы можаце пазначыць пэўную дату (“2008-01-15”) ці адносную (“2 years 1 day 3 minutes ago”).

Таксама вы маеце магчымасьць фільтраваць сьпіс камітаў па зададзенай умове. Опцыя `--author` задае імя аўтара, а `--grep` дазваляе выводзіць каміты з ключавымі словамі ў паведамленьні. (Зьвярніце ўвагу на тое, што калі вы жадаеце пазначыць абедзьве опцыі, вы мусіце дадаць опцыю `--all-match`.)

Апошняя сапраўды карысная опцыя — гэта шлях. Калі вы пазначаеце імя дырэкторыі ці фала, вы абмяжоўваеце вывад толькі тымі камітамі, якія ўносяць зьмены ў гэтыя файлы. Гэта опцыя заўсёды павінна быць апошняй і папярэджваецца дзьвюма злучкамі (`--`) каб разьдзяліць шлях і астатнія парамэтры.

У Табліцы 2-3 прыведзены сьпіс часта ўжываных опцыяў.

	Опцыя	Апісаньне
	-(n)	Адлюстраваць толькі апошнія n камітаў
	--since, --after	Limit the commits to those made after the specified date.
	--until, --before	Limit the commits to those made before the specified date.
	--author	Only show commits in which the author entry matches the specified string.
	--committer	Only show commits in which the committer entry matches the specified string.

For example, if you want to see which commits modifying test files in the Git source code history were committed by Junio Hamano and were not merges in the month of October 2008, you can run something like this:

	$ git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \
	   --before="2008-11-01" --no-merges -- t/
	5610e3b - Fix testcase failure when extended attribute
	acd3b9e - Enhance hold_lock_file_for_{update,append}()
	f563754 - demonstrate breakage of detached checkout wi
	d1a43f2 - reset --hard/read-tree --reset -u: remove un
	51a94af - Fix "checkout --track -b newbranch" on detac
	b0ad11e - pull: allow "git pull origin $something:$cur

Of the nearly 20,000 commits in the Git source code history, this command shows the 6 that match those criteria.

### Using a GUI to Visualize History ###

If you like to use a more graphical tool to visualize your commit history, you may want to take a look at a Tcl/Tk program called `gitk` that is distributed with Git. Gitk is basically a visual `git log` tool, and it accepts nearly all the filtering options that `git log` does. If you type `gitk` on the command line in your project, you should see something like Figure 2-2.

Insert 18333fig0202.png
Figure 2-2. The gitk history visualizer.

You can see the commit history in the top half of the window along with a nice ancestry graph. The diff viewer in the bottom half of the window shows you the changes introduced at any commit you click.

## Undoing Things ##

At any stage, you may want to undo something. Here, we’ll review a few basic tools for undoing changes that you’ve made. Be careful, because you can’t always revert some of these undos. This is one of the few areas in Git where you may lose some work if you do it wrong.

### Changing Your Last Commit ###

One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. If you want to try that commit again, you can run commit with the `--amend` option:

	$ git commit --amend

This command takes your staging area and uses it for the commit. If you’ve made no changes since your last commit (for instance, you run this command immediately after your previous commit), then your snapshot will look exactly the same and all you’ll change is your commit message.

The same commit-message editor fires up, but it already contains the message of your previous commit. You can edit the message the same as always, but it overwrites your previous commit.

As an example, if you commit and then realize you forgot to stage the changes in a file you wanted to add to this commit, you can do something like this:

	$ git commit -m 'initial commit'
	$ git add forgotten_file
	$ git commit --amend

After these three commands, you end up with a single commit — the second commit replaces the results of the first.

### Unstaging a Staged File ###

The next two sections demonstrate how to wrangle your staging area and working directory changes. The nice part is that the command you use to determine the state of those two areas also reminds you how to undo changes to them. For example, let’s say you’ve changed two files and want to commit them as two separate changes, but you accidentally type `git add *` and stage them both. How can you unstage one of the two? The `git status` command reminds you:

	$ git add .
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#       modified:   README.txt
	#       modified:   benchmarks.rb
	#

Right below the “Changes to be committed” text, it says "use `git reset HEAD <file>...` to unstage". So, let’s use that advice to unstage the `benchmarks.rb` file:

	$ git reset HEAD benchmarks.rb
	benchmarks.rb: locally modified
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#       modified:   README.txt
	#
	# Changed but not updated:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#       modified:   benchmarks.rb
	#

The command is a bit strange, but it works. The `benchmarks.rb` file is modified but once again unstaged.

### Unmodifying a Modified File ###

What if you realize that you don’t want to keep your changes to the `benchmarks.rb` file? How can you easily unmodify it — revert it back to what it looked like when you last committed (or initially cloned, or however you got it into your working directory)? Luckily, `git status` tells you how to do that, too. In the last example output, the unstaged area looks like this:

	# Changed but not updated:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#       modified:   benchmarks.rb
	#

It tells you pretty explicitly how to discard the changes you’ve made (at least, the newer versions of Git, 1.6.1 and later, do this — if you have an older version, we highly recommend upgrading it to get some of these nicer usability features). Let’s do what it says:

	$ git checkout -- benchmarks.rb
	$ git status
	# On branch master
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#       modified:   README.txt
	#

You can see that the changes have been reverted. You should also realize that this is a dangerous command: any changes you made to that file are gone — you just copied another file over it. Don’t ever use this command unless you absolutely know that you don’t want the file. If you just need to get it out of the way, we’ll go over stashing and branching in the next chapter; these are generally better ways to go.

Remember, anything that is committed in Git can almost always be recovered. Even commits that were on branches that were deleted or commits that were overwritten with an `--amend` commit can be recovered (see *Chapter 9* for data recovery). However, anything you lose that was never committed is likely never to be seen again.

## Working with Remotes ##

To be able to collaborate on any Git project, you need to know how to manage your remote repositories. Remote repositories are versions of your project that are hosted on the Internet or network somewhere. You can have several of them, each of which generally is either read-only or read/write for you. Collaborating with others involves managing these remote repositories and pushing and pulling data to and from them when you need to share work.
Managing remote repositories includes knowing how to add remote repositories, remove remotes that are no longer valid, manage various remote branches and define them as being tracked or not, and more. In this section, we’ll cover these remote-management skills.

### Showing Your Remotes ###

To see which remote servers you have configured, you can run the `git remote` command. It lists the shortnames of each remote handle you’ve specified. If you’ve cloned your repository, you should at least see *origin* — that is the default name Git gives to the server you cloned from:

	$ git clone git://github.com/schacon/ticgit.git
	Initialized empty Git repository in /private/tmp/ticgit/.git/
	remote: Counting objects: 595, done.
	remote: Compressing objects: 100% (269/269), done.
	remote: Total 595 (delta 255), reused 589 (delta 253)
	Receiving objects: 100% (595/595), 73.31 KiB | 1 KiB/s, done.
	Resolving deltas: 100% (255/255), done.
	$ cd ticgit
	$ git remote
	origin

You can also specify `-v`, which shows you the URL that Git has stored for the shortname to be expanded to:

	$ git remote -v
	origin	git://github.com/schacon/ticgit.git

If you have more than one remote, the command lists them all. For example, my Grit repository looks something like this.

	$ cd grit
	$ git remote -v
	bakkdoor  git://github.com/bakkdoor/grit.git
	cho45     git://github.com/cho45/grit.git
	defunkt   git://github.com/defunkt/grit.git
	koke      git://github.com/koke/grit.git
	origin    git@github.com:mojombo/grit.git

This means we can pull contributions from any of these users pretty easily. But notice that only the origin remote is an SSH URL, so it’s the only one I can push to (we’ll cover why this is in *Chapter 4*).

### Adding Remote Repositories ###

I’ve mentioned and given some demonstrations of adding remote repositories in previous sections, but here is how to do it explicitly. To add a new remote Git repository as a shortname you can reference easily, run `git remote add [shortname] [url]`:

	$ git remote
	origin
	$ git remote add pb git://github.com/paulboone/ticgit.git
	$ git remote -v
	origin	git://github.com/schacon/ticgit.git
	pb	git://github.com/paulboone/ticgit.git

Now you can use the string `pb` on the command line in lieu of the whole URL. For example, if you want to fetch all the information that Paul has but that you don’t yet have in your repository, you can run git fetch pb:

	$ git fetch pb
	remote: Counting objects: 58, done.
	remote: Compressing objects: 100% (41/41), done.
	remote: Total 44 (delta 24), reused 1 (delta 0)
	Unpacking objects: 100% (44/44), done.
	From git://github.com/paulboone/ticgit
	 * [new branch]      master     -> pb/master
	 * [new branch]      ticgit     -> pb/ticgit

Paul’s master branch is accessible locally as `pb/master` — you can merge it into one of your branches, or you can check out a local branch at that point if you want to inspect it.

### Fetching and Pulling from Your Remotes ###

As you just saw, to get data from your remote projects, you can run:

	$ git fetch [remote-name]

The command goes out to that remote project and pulls down all the data from that remote project that you don’t have yet. After you do this, you should have references to all the branches from that remote, which you can merge in or inspect at any time. (We’ll go over what branches are and how to use them in much more detail in *Chapter 3*.)

If you clone a repository, the command automatically adds that remote repository under the name *origin*. So, `git fetch origin` fetches any new work that has been pushed to that server since you cloned (or last fetched from) it. It’s important to note that the `fetch` command pulls the data to your local repository — it doesn’t automatically merge it with any of your work or modify what you’re currently working on. You have to merge it manually into your work when you’re ready.

If you have a branch set up to track a remote branch (see the next section and *Chapter 3* for more information), you can use the `git pull` command to automatically fetch and then merge a remote branch into your current branch. This may be an easier or more comfortable workflow for you; and by default, the `git clone` command automatically sets up your local master branch to track the remote master branch on the server you cloned from (assuming the remote has a master branch). Running `git pull` generally fetches data from the server you originally cloned from and automatically tries to merge it into the code you’re currently working on.

### Pushing to Your Remotes ###

When you have your project at a point that you want to share, you have to push it upstream. The command for this is simple: `git push [remote-name] [branch-name]`. If you want to push your master branch to your `origin` server (again, cloning generally sets up both of those names for you automatically), then you can run this to push your work back up to the server:

	$ git push origin master

This command works only if you cloned from a server to which you have write access and if nobody has pushed in the meantime. If you and someone else clone at the same time and they push upstream and then you push upstream, your push will rightly be rejected. You’ll have to pull down their work first and incorporate it into yours before you’ll be allowed to push. See *Chapter 3* for more detailed information on how to push to remote servers.

### Inspecting a Remote ###

If you want to see more information about a particular remote, you can use the `git remote show [remote-name]` command. If you run this command with a particular shortname, such as `origin`, you get something like this:

	$ git remote show origin
	* remote origin
	  URL: git://github.com/schacon/ticgit.git
	  Remote branch merged with 'git pull' while on branch master
	    master
	  Tracked remote branches
	    master
	    ticgit

It lists the URL for the remote repository as well as the tracking branch information. The command helpfully tells you that if you’re on the master branch and you run `git pull`, it will automatically merge in the master branch on the remote after it fetches all the remote references. It also lists all the remote references it has pulled down.

That is a simple example you’re likely to encounter. When you’re using Git more heavily, however, you may see much more information from `git remote show`:

	$ git remote show origin
	* remote origin
	  URL: git@github.com:defunkt/github.git
	  Remote branch merged with 'git pull' while on branch issues
	    issues
	  Remote branch merged with 'git pull' while on branch master
	    master
	  New remote branches (next fetch will store in remotes/origin)
	    caching
	  Stale tracking branches (use 'git remote prune')
	    libwalker
	    walker2
	  Tracked remote branches
	    acl
	    apiv2
	    dashboard2
	    issues
	    master
	    postgres
	  Local branch pushed with 'git push'
	    master:master

This command shows which branch is automatically pushed when you run `git push` on certain branches. It also shows you which remote branches on the server you don’t yet have, which remote branches you have that have been removed from the server, and multiple branches that are automatically merged when you run `git pull`.

### Removing and Renaming Remotes ###

If you want to rename a reference, in newer versions of Git you can run `git remote rename` to change a remote’s shortname. For instance, if you want to rename `pb` to `paul`, you can do so with `git remote rename`:

	$ git remote rename pb paul
	$ git remote
	origin
	paul

It’s worth mentioning that this changes your remote branch names, too. What used to be referenced at `pb/master` is now at `paul/master`.

If you want to remove a reference for some reason — you’ve moved the server or are no longer using a particular mirror, or perhaps a contributor isn’t contributing anymore — you can use `git remote rm`:

	$ git remote rm paul
	$ git remote
	origin

## Tagging ##

Like most VCSs, Git has the ability to tag specific points in history as being important. Generally, people use this functionality to mark release points (`v1.0`, and so on). In this section, you’ll learn how to list the available tags, how to create new tags, and what the different types of tags are.

### Listing Your Tags ###

Listing the available tags in Git is straightforward. Just type `git tag`:

	$ git tag
	v0.1
	v1.3

This command lists the tags in alphabetical order; the order in which they appear has no real importance.

You can also search for tags with a particular pattern. The Git source repo, for instance, contains more than 240 tags. If you’re only interested in looking at the 1.4.2 series, you can run this:

	$ git tag -l 'v1.4.2.*'
	v1.4.2.1
	v1.4.2.2
	v1.4.2.3
	v1.4.2.4

### Creating Tags ###

Git uses two main types of tags: lightweight and annotated. A lightweight tag is very much like a branch that doesn’t change — it’s just a pointer to a specific commit. Annotated tags, however, are stored as full objects in the Git database. They’re checksummed; contain the tagger name, e-mail, and date; have a tagging message; and can be signed and verified with GNU Privacy Guard (GPG). It’s generally recommended that you create annotated tags so you can have all this information; but if you want a temporary tag or for some reason don’t want to keep the other information, lightweight tags are available too.

### Annotated Tags ###

Creating an annotated tag in Git is simple. The easiest way is to specify `-a` when you run the `tag` command:

	$ git tag -a v1.4 -m 'my version 1.4'
	$ git tag
	v0.1
	v1.3
	v1.4

The `-m` specifies a tagging message, which is stored with the tag. If you don’t specify a message for an annotated tag, Git launches your editor so you can type it in.

You can see the tag data along with the commit that was tagged by using the `git show` command:

	$ git show v1.4
	tag v1.4
	Tagger: Scott Chacon <schacon@gee-mail.com>
	Date:   Mon Feb 9 14:45:11 2009 -0800

	my version 1.4
	commit 15027957951b64cf874c3557a0f3547bd83b3ff6
	Merge: 4a447f7... a6b4c97...
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Sun Feb 8 19:02:46 2009 -0800

	    Merge branch 'experiment'

That shows the tagger information, the date the commit was tagged, and the annotation message before showing the commit information.

### Signed Tags ###

You can also sign your tags with GPG, assuming you have a private key. All you have to do is use `-s` instead of `-a`:

	$ git tag -s v1.5 -m 'my signed 1.5 tag'
	You need a passphrase to unlock the secret key for
	user: "Scott Chacon <schacon@gee-mail.com>"
	1024-bit DSA key, ID F721C45A, created 2009-02-09

If you run `git show` on that tag, you can see your GPG signature attached to it:

	$ git show v1.5
	tag v1.5
	Tagger: Scott Chacon <schacon@gee-mail.com>
	Date:   Mon Feb 9 15:22:20 2009 -0800

	my signed 1.5 tag
	-----BEGIN PGP SIGNATURE-----
	Version: GnuPG v1.4.8 (Darwin)

	iEYEABECAAYFAkmQurIACgkQON3DxfchxFr5cACeIMN+ZxLKggJQf0QYiQBwgySN
	Ki0An2JeAVUCAiJ7Ox6ZEtK+NvZAj82/
	=WryJ
	-----END PGP SIGNATURE-----
	commit 15027957951b64cf874c3557a0f3547bd83b3ff6
	Merge: 4a447f7... a6b4c97...
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Sun Feb 8 19:02:46 2009 -0800

	    Merge branch 'experiment'

A bit later, you’ll learn how to verify signed tags.

### Lightweight Tags ###

Another way to tag commits is with a lightweight tag. This is basically the commit checksum stored in a file — no other information is kept. To create a lightweight tag, don’t supply the `-a`, `-s`, or `-m` option:

	$ git tag v1.4-lw
	$ git tag
	v0.1
	v1.3
	v1.4
	v1.4-lw
	v1.5

This time, if you run `git show` on the tag, you don’t see the extra tag information. The command just shows the commit:

	$ git show v1.4-lw
	commit 15027957951b64cf874c3557a0f3547bd83b3ff6
	Merge: 4a447f7... a6b4c97...
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Sun Feb 8 19:02:46 2009 -0800

	    Merge branch 'experiment'

### Verifying Tags ###

To verify a signed tag, you use `git tag -v [tag-name]`. This command uses GPG to verify the signature. You need the signer’s public key in your keyring for this to work properly:

	$ git tag -v v1.4.2.1
	object 883653babd8ee7ea23e6a5c392bb739348b1eb61
	type commit
	tag v1.4.2.1
	tagger Junio C Hamano <junkio@cox.net> 1158138501 -0700

	GIT 1.4.2.1

	Minor fixes since 1.4.2, including git-mv and git-http with alternates.
	gpg: Signature made Wed Sep 13 02:08:25 2006 PDT using DSA key ID F3119B9A
	gpg: Good signature from "Junio C Hamano <junkio@cox.net>"
	gpg:                 aka "[jpeg image of size 1513]"
	Primary key fingerprint: 3565 2A26 2040 E066 C9A7  4A7D C0C6 D9A4 F311 9B9A

If you don’t have the signer’s public key, you get something like this instead:

	gpg: Signature made Wed Sep 13 02:08:25 2006 PDT using DSA key ID F3119B9A
	gpg: Can't check signature: public key not found
	error: could not verify the tag 'v1.4.2.1'

### Tagging Later ###

You can also tag commits after you’ve moved past them. Suppose your commit history looks like this:

	$ git log --pretty=oneline
	15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
	a6b4c97498bd301d84096da251c98a07c7723e65 beginning write support
	0d52aaab4479697da7686c15f77a3d64d9165190 one more thing
	6d52a271eda8725415634dd79daabbc4d9b6008e Merge branch 'experiment'
	0b7434d86859cc7b8c3d5e1dddfed66ff742fcbc added a commit function
	4682c3261057305bdd616e23b64b0857d832627b added a todo file
	166ae0c4d3f420721acbb115cc33848dfcc2121a started write support
	9fceb02d0ae598e95dc970b74767f19372d61af8 updated rakefile
	964f16d36dfccde844893cac5b347e7b3d44abbc commit the todo
	8a5cbc430f1a9c3d00faaeffd07798508422908a updated readme

Now, suppose you forgot to tag the project at `v1.2`, which was at the "updated rakefile" commit. You can add it after the fact. To tag that commit, you specify the commit checksum (or part of it) at the end of the command:

	$ git tag -a v1.2 9fceb02

You can see that you’ve tagged the commit:

	$ git tag
	v0.1
	v1.2
	v1.3
	v1.4
	v1.4-lw
	v1.5

	$ git show v1.2
	tag v1.2
	Tagger: Scott Chacon <schacon@gee-mail.com>
	Date:   Mon Feb 9 15:32:16 2009 -0800

	version 1.2
	commit 9fceb02d0ae598e95dc970b74767f19372d61af8
	Author: Magnus Chacon <mchacon@gee-mail.com>
	Date:   Sun Apr 27 20:43:35 2008 -0700

	    updated rakefile
	...

### Sharing Tags ###

By default, the `git push` command doesn’t transfer tags to remote servers. You will have to explicitly push tags to a shared server after you have created them.  This process is just like sharing remote branches — you can run `git push origin [tagname]`.

	$ git push origin v1.5
	Counting objects: 50, done.
	Compressing objects: 100% (38/38), done.
	Writing objects: 100% (44/44), 4.56 KiB, done.
	Total 44 (delta 18), reused 8 (delta 1)
	To git@github.com:schacon/simplegit.git
	* [new tag]         v1.5 -> v1.5

If you have a lot of tags that you want to push up at once, you can also use the `--tags` option to the `git push` command.  This will transfer all of your tags to the remote server that are not already there.

	$ git push origin --tags
	Counting objects: 50, done.
	Compressing objects: 100% (38/38), done.
	Writing objects: 100% (44/44), 4.56 KiB, done.
	Total 44 (delta 18), reused 8 (delta 1)
	To git@github.com:schacon/simplegit.git
	 * [new tag]         v0.1 -> v0.1
	 * [new tag]         v1.2 -> v1.2
	 * [new tag]         v1.4 -> v1.4
	 * [new tag]         v1.4-lw -> v1.4-lw
	 * [new tag]         v1.5 -> v1.5

Now, when someone else clones or pulls from your repository, they will get all your tags as well.

## Tips and Tricks ##

Before we finish this chapter on basic Git, a few little tips and tricks may make your Git experience a bit simpler, easier, or more familiar. Many people use Git without using any of these tips, and we won’t refer to them or assume you’ve used them later in the book; but you should probably know how to do them.

### Auto-Completion ###

If you use the Bash shell, Git comes with a nice auto-completion script you can enable. Download the Git source code, and look in the `contrib/completion` directory; there should be a file called `git-completion.bash`. Copy this file to your home directory, and add this to your `.bashrc` file:

	source ~/.git-completion.bash

If you want to set up Git to automatically have Bash shell completion for all users, copy this script to the `/opt/local/etc/bash_completion.d` directory on Mac systems or to the `/etc/bash_completion.d/` directory on Linux systems. This is a directory of scripts that Bash will automatically load to provide shell completions.

If you’re using Windows with Git Bash, which is the default when installing Git on Windows with msysGit, auto-completion should be preconfigured.

Press the Tab key when you’re writing a Git command, and it should return a set of suggestions for you to pick from:

	$ git co<tab><tab>
	commit config

In this case, typing `git co` and then pressing the Tab key twice suggests commit and config. Adding `m<tab>` completes `git commit` automatically.

This also works with options, which is probably more useful. For instance, if you’re running a `git log` command and can’t remember one of the options, you can start typing it and press Tab to see what matches:

	$ git log --s<tab>
	--shortstat  --since=  --src-prefix=  --stat   --summary

That’s a pretty nice trick and may save you some time and documentation reading.

### Git Aliases ###

Git doesn’t infer your command if you type it in partially. If you don’t want to type the entire text of each of the Git commands, you can easily set up an alias for each command using `git config`. Here are a couple of examples you may want to set up:

	$ git config --global alias.co checkout
	$ git config --global alias.br branch
	$ git config --global alias.ci commit
	$ git config --global alias.st status

This means that, for example, instead of typing `git commit`, you just need to type `git ci`. As you go on using Git, you’ll probably use other commands frequently as well; in this case, don’t hesitate to create new aliases.

This technique can also be very useful in creating commands that you think should exist. For example, to correct the usability problem you encountered with unstaging a file, you can add your own unstage alias to Git:

	$ git config --global alias.unstage 'reset HEAD --'

This makes the following two commands equivalent:

	$ git unstage fileA
	$ git reset HEAD fileA

This seems a bit clearer. It’s also common to add a `last` command, like this:

	$ git config --global alias.last 'log -1 HEAD'

This way, you can see the last commit easily:

	$ git last
	commit 66938dae3329c7aebe598c2246a8e6af90d04646
	Author: Josh Goebel <dreamer3@example.com>
	Date:   Tue Aug 26 19:48:51 2008 +0800

	    test for current head

	    Signed-off-by: Scott Chacon <schacon@example.com>

As you can tell, Git simply replaces the new command with whatever you alias it to. However, maybe you want to run an external command, rather than a Git subcommand. In that case, you start the command with a `!` character. This is useful if you write your own tools that work with a Git repository. We can demonstrate by aliasing `git visual` to run `gitk`:

	$ git config --global alias.visual "!gitk"

## Summary ##

At this point, you can do all the basic local Git operations — creating or cloning a repository, making changes, staging and committing those changes, and viewing the history of all the changes the repository has been through. Next, we’ll cover Git’s killer feature: its branching model.
