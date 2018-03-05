<a name="top"></a>
# Performance in webbasierten Anwendungen
<a href="https://github.com/th-koeln/wba1-2015/wiki/Performance-Ausarbeitung_FuchshoferKollig_Deckblatt" target="_blank">*Deckblatt*<a/>

## Inhaltsverzeichnis




1. [**Einleitung**](#einleitung)     
2. [**Performance in webbasierten Anwendungen**](#performance)   
2.1 [Gründe für die Performance Optimierung](#gruende)   
2.2 [Performance Tests](#tests)                                  
3. [**Performance Optimierung**](#moeglichkeit)   
3.1 [Caching](#cache)         
3.2 [Anfragen optimieren (HTTP-Requests)](#anfragen)         
3.3 [CSS und JavaScript optimieren](#cssjavascript)         
3.4 [Bilddateien optimieren](#bilddateien)    
3.5 [State Handling](#statehandling)      
4. [**Wahrgenommene Performance**](#wahrgenommen)  
5. [**Was kann der User tun?**](#user)
6. [**Fazit**](#fazit)
7. [**Quellen**](#quellen)
8. [**Abbildungsverzeichnis**](#abbildungsverzeichnis)  






<a name="einleitung"></a>
## 1 Einleitung  

Die Performance (engl. Durchführung, Aufführung, Darstellung, Leistung) ist laut Definition das Verhalten eines Softwareprodukts bei der Ausführung. Performance, oder auch einfach Rechenleistung genannt, spielt in vielen verschiedenen Bereichen eine Rolle, wie z.B. in einzelnen Hardwarekomponenten (Grafikkarte, CPU, Arbeitsspeicher), Software (Ablaufgeschwindigkeit von Code) oder großen IT-Systemen wie Serversysteme, Großrechner und Superrechner. Dabei ist mit der Performance meistens die Datenverarbeitungsgeschwindigkeit (Berechnungen/Zeiteinheit) gemeint wobei sie für den einfachen User durch das schnelle (oder auch langsame) laden von Programmen, Websites oder Daten definiert wird.
Durch das Internet und die immer fortschreitende Technologien steigt auch die Erwartung des Users, dass Informationen schneller abrufbar, und Programme schneller ausführbar sind. Performance lässt sich in drei Faktoren unterteilen.
     
1. **Server Performance**   
Befasst sich mit der Zeit, die Webserver brauchen um Anfragen zu bearbeiten.   
2. **Netzwerk Performance**   
Befasst sich mit der Übertragung von Informationen auf der Netzwerkebene und der Infrastruktur des Internets.   
3. **Front End Performance**   
Beschäftigt sich mit der Clientseitigen Verarbeitung von Daten z.B. die Darstellung im Browser.   

In Webanwendungen unterscheidet man auch weiter in:
   
1. **Empirische Performance**   
Die Ladezeit von Daten wird einfach in Zahlen gemessen und präsentiert.   
2. **Psychologische Performance**   
Es wird analysiert, welche Inhalte zuerst angezeigt werden und welche eine kurze oder lange Ladezeit haben. Das ist wichtig, da die [Wahrgenommene Performance](#wahrgenommen) der Ladezeit und der Aufbau einer Website für den Nutzer von großer Bedeutung sind.   

[*Startseite*](#top)



<a name="performance"></a>
## 2 Performance in webbasierten Anwendungen


Die Performance einer Webanwendung ist vor allem für den Endnutzer sehr wichtig und interessant.  Durch einen schnellen Aufbau einer Website wird dem Nutzer ermöglicht schnell Informationen abrufen zu können. Die durch das Internet ausgelöste, mittlerweile sehr schnelllebige Welt bringt vor allem die Nutzer dazu die Anforderung zu stellen, Informationen oder Daten auf Knopfdruck schnell geliefert zu bekommen. Demzufolge obliegt es den Programmierern und Systemadministratoren eine Technik zur Verfügung zu stellen, mit der diese Bedürfnisse gestillt werden können. Im Folgenden beschränken wir uns auf die Technik und Möglichkeiten die den Entwicklern und Administratoren zur Verfügung stehen, um den schnellen Aufruf von Webanwendungen wie Websites zu ermöglichen. Die Tatsache,  dass der langsame Aufbau einer Website auch oft am Endgerät oder der Internetgeschwindigkeit des Nutzers liegt, stellen wir aus diesem Grund hinten an.
Webanwendungen im Allgemeinen arbeiten mit einem einfachen Request/Response-Mechanismus auf Basis des HTTP-Protokolls, dass eine Darstellung im Web ermöglicht. Der Nutzer (bzw. der Browser) schickt eine Anfrage(Request) an einen bestimmten Server und erhält eine Antwort(Response) die ihm die möglichen Informationen liefert.  Der Server verarbeitet die Anfrage in einem oder mehreren Threads und liefert das Ergebnis an den Browser zurück, der daraus sichtbare Elemente auf dem Bildschirm des Users rendert. Allein dieser einfache Weg bietet aber schon eine Vielzahl an Fehlerquellen die zu schlechter Performance führen können. Auf der Seite des Nutzers (wenn auch nicht durch den Nutzer verschuldet), können HTML Rendering Probleme oder schlecht umgesetzter JavaScript Code ein fehlerhaftes Darstellen oder lange Wartezeit verursachen. Das Netzwerk über das die Informationen ausgetauscht werden birgt außerdem die Gefahr das eine hohe Latenz, hohes Datenvolumen oder eine hohe Anzahl von „AJAX Calls“ die Verbindung beeinträchtigt. Auf Seiten des Servers findet sich außerdem eine Vielzahl an Fehlerquellen  wie Datenbank Zugriffsfehler, eine hohe Anzahl an Backend Calls oder Thread-/Connectionpool- Probleme, hervorgerufen durch wiederum eine Vielzahl an Fehlermöglichkeiten.
Zusätzlich können zu den oben genannten Problemen noch fehlendes oder falsches Caching, eine zu große Anzahl an Requests an den Server, schlechte Garbage Collector Einstellungen, falsches State Handling oder langlaufende synchrone Aufrufe zu Verringerung der Performance für den Nutzer führen.
  

<a name="abb001"></a>
![Abbildung 1](https://www.codecentric.de/files/2011/05/ueberblick-ueber-performanceprobleme-bei-webanwendungen.png)   
[Abbildung 1: Probleme, die bei Webanwendungen zu Performanceverlust führen können](#abbildungsverzeichnis)   

[*Startseite*](#top)


<a name="gruende"></a>
#### 2.1 Gründe für die Performance Optimierung


Einer der wohl wichtigsten Gründe sich mit der Performance von Webanwendungen zu beschäftigen ist der Kostenfaktor. Eine Website mit schlechter Performance spielt unter Umständen weniger Gewinn ein, da Nutzer nur langsam oder gar nicht auf den Content und die Funktionen der Webanwendung zugreifen können. Das bedeutet weniger Interessenten, weniger Aufrufe, weniger Umsatz (sofern mit dieser Website Geld verdient wird). Für große Unternehmen ist eine gut funktionierende und vor allem schnell aufrufbare Website sehr wichtig, da in den meisten Fällen mit ihr das Image der Firma repräsentiert wird. Onlineshops sind besonders von einer guten Performance ihrer Website und der schnellen Datenübertragung abhängig, da Studien belegen, dass eine schnellere Website auch mehr Kaufabschlüsse mit sich bringt.
Aber auch der einfache Nutzer möchte nicht „ewig“ auf den Content einer Website warten, sondern schnell Zugriff bekommen. Schließlich ist das Internet bekannt dafür, eine schnelle und einfache Möglichkeit zu bieten, Informationen über jegliche Themenbereiche zu bekommen. Des weiteren zeigen Studien das Nutzer meist schon nach ein paar Sekunden die Seite wieder verlassen, falls diese bis dahin nicht geladen und der Content einsehbar ist.
Ein anderer Grund sind die Betriebskosten. Um Content der breiten Masse zur Verfügung zu stellen braucht man einen oder besser mehrere Server an verschiedenen Standpunkten. Ein Performance optimierter Server braucht weniger Hardware und schafft es, mit weniger Ressourcen mehr Anfragen bearbeiten zu können. Das spart bei entsprechend hoher Nutzung eine Menge Geld und Energie ein. Des weiteren wird der Wartungsaufwand reduziert, was eine geringere Fehleranfälligkeit und weniger Ausgaben für Wartungspersonal zur Folge hat.
Suchmaschinenoptimierung (<a href="http://static.googleusercontent.com/media/www.google.de/de/de/webmasters/docs/einfuehrung-in-suchmaschinenoptimierung.pdf" target="_blank">SEO<a/>, engl. search engine optimation) ist ein weiterer wichtiger Punkt für die Steigerung der Performance einer Website. Es ist allgemein bekannt das Google das Ranking anhand der Schnelligkeit der Websites festlegt. So werden sich schnell aufbauende Websites in der Regel dafür belohnt und im Ranking weiter oben angezeigt. Für die Präsenz einer Website ist das heutzutage äußerst wichtig, da Google als meist besuchte Website zählt und somit ausschlaggebend für die Suche nach neuen Websites bzw. dessen Content ist.

[*Startseite*](#top)

<a name="tests"></a>
#### 2.2 Performance Tests



Um die Performance in Webanwendungen effektiv verbessern zu können, muss man erst einmal wissen wo Probleme auftreten können. Es gibt zahlreiche Tools wie
<a href="http://loaduiweb.org/" target="_blank">LoadUIWeb</a> ,  <a href="http://grinder.sourceforge.net/" target="_blank">The Grinder</a> oder <a href="http://jmeter.apache.org/index.html" target="_blank">JMeter</a>. die sich auf Performancetests und Analyse spezialisiert haben, wobei <a href="https://www.google.com/intl/de_de/analytics/" target="_blank">Google Analytics</a> die wohl bekannteste Möglichkeit zur Webanalyse ist. Einfache Lasttests rufen z.B. die Startseite einer Website X mal auf und liefern danach ein Testergebnis das Rückschlüsse auf die Geschwindigkeit einer Website liefert. Da die meisten modernen Websites aber vielschichtig sind und aus mehreren Seiten und Navigationspunkten zu externen Websites bestehen, ist so ein Testergebnis meist nur für den groben Überblick zu gebrauchen.
Große Lasttests sollten möglichst realistisch gestaltet werden. Es sollte eine Simulation erstellt werden, bei der eine realistische Anzahl an Usern gleichzeitig auf verschiedene Komponenten der Website zugreifen um zu überprüfen ob der Server mit der hohen Anzahl an Anfragen zurechtkommt.
JMeter kommt mit einer Vielzahl an Tests und Analysetools, mit dem man Ablaufpläne erstellen kann, welche auf einer Website ausgeführt werden sollen. Ein Testplan besteht u.a. aus folgenden Komponenten:      

1.	**Threadgruppen**         
Es werden Gruppen von Aufgaben erstellt, die nacheinander oder simultan mit einer bestimmten Häufigkeit ausgeführt werden.      
2.	**HTTP Request**         
Hier können mit GET und POST Variablen die Aufrufe von bestimmten Websites festgelegt werden.   
3.	**Versicherte Antwort**         
Um zu testen, ob eine Seite auch das zurückgibt, wofür sie konzipiert wurde, gibt es den Punkt „Versicherte Antwort“, die überprüft ob unter Volllast nicht etwa eine falsche Seite zurückgegeben wird.
Um die Ergebnisse dieses Tests anzuzeigen, gibt es unter „JMeter“ verschiedene GUI die eine detaillierte Auswertung anzeigen.         

[*Startseite*](#top)

<a name="moeglichkeit"></a>
## 3 Performance Optimierungen


Möchte man die Performance einer Webanwendung steigern, da sie z.B. zu lange Ladezeiten aufweist oder zu viele Ressourcen beansprucht so dass sich kein guter Kosten/Nutzen Faktor ergibt, hat man sehr viele Möglichkeiten dies zu tun. Aufgrund der Tatsache das es sehr viele mögliche Fehlerquellen gibt die die Performance beeinflussen, hat man viele Punkte gegeben, an denen man bei der Optimierung ansetzen kann. Im Folgenden werden einige Probleme aufgeführt die die Performance beeinflussen, und Beispiele  genannt, wie diese behoben werden können.  

[*Startseite*](#top)

<a name="cache"></a>
#### 3.1 Caching


<a href="https://de.wikipedia.org/wiki/Cache" target="_blank">Caching</a> (engl. zwischenspeichern) bedeutet Websites z.B. im Browserchache zwischenzuspeichern, damit diese bei wiederholtem Aufrufen schneller verfügbar sind. Genau aus dem Grund ist es ein sehr wichtiger Faktor wenn man die Performance einer Webanwendung sinnvoll steigern will. Durch das Speichern von Daten im Browser-Cache wird verhindert das diese ständig per Request angefragt werden, was die Zugriffszeit erhöhen, und somit die Datenübertragung unnötig belasten würde. Durch das geschickte einsetzen von Puffer-Speichern (Cache), lassen sich Daten bei Bedarf schneller abrufen, da sie entweder durch eine vorherige Anfrage an den Server noch verfügbar sind, oder schon vorab geladen wurden, wenn absehbar ist das sie demnächst benötigt werden.
Caching ist somit wohl offensichtlich ein Allheilmittel wenn eine Anwendung langsam laufen sollte und nicht die nötige Leistung liefert. Allerdings ist zu beachten, dass zu viel cachen eher hinderlich ist denn  dadurch würden nämlich z.B. alle möglichen Daten schon vorab geladen werden, welche vielleicht gar nicht benötigt werden. Das würde beim ersten Aufrufen einer Website zu langen Ladezeiten führen da alle möglichen Daten erst einmal geladen werden. Desweiteren sind dynamische Daten die oft geändert werden im Cache eher eine Leistungsbremse, da sie ständig neu abgefragt werden und somit zu einer hohen Anzahl an Requests führen.   

[*Startseite*](#top)


<a name="anfragen"></a>
#### 3.2 Anfragen optimieren (HTTP-Request)


Ein wesentliches Problem das schon bei der Konzeption der Webanwendung angegangen wird, ist die Möglichkeit der zu vielen gleichzeitigen Zugriffe auf einen Server.
Im Idealfall interessieren sich viele Nutzer für bspw. eine Website und dessen Content. Damit ist aber automatisch verbunden das eine hohe Anzahl an Requests an den Server gesandt werden. Bei der Konzeption und Entwicklung wird meist schon sehr früh auf dieses Thema eingegangen, da es einen oder mehrere gute Server voraussetzen. Der Kosten-Nutzen Faktor ist hier aber ebenfalls unbedingt zu beachten, da Ressourcen nicht kostenlos sind. Eine Unterschätzung der Zugriffslast auf eine Website hat zufolge das Anfragen nicht mehr zeitnah bearbeitet werden können und der Nutzer unter Umständen sehr lange auf den Response des Servers warten muss.
Jede Interaktion die der Nutzer in einer Webanwendung tätigen kann, hat in der Regel zu Folge, dass ein Request an einen Server geschickt wird um Informationen zu erhalten.
Der Grundsatz jeder Webanwendung liegt darin, dass die Anzahl der Interaktionen so gering wie möglich gehalten wird! Zu viele mögliche Interaktionen haben gegebenenfalls zur Folge, dass eine hohe Server- oder Netzwerkbelastung vorliegt, was in der Regel zu starken Performance Einbrüchen führt.
Die gängigen Browser wie Firefox, Google Chrome, Safari oder Opera bieten die Möglichkeit eine bestimmte Anzahl an Anfragen parallel zu bearbeiten. Je mehr Anfragen von einem Browser an einen Server geschickt werden, desto langsamer wird der Seitenaufbau, da nur eine bestimmte Anzahl an Requests gleichzeitig bearbeitet werden können und der Rest warten muss. In [Abbildung 2](#abb002) wird aufgelistet wie viele Anfragen die verschiedenen Browser gleichzeit tätigen können.  

<a name="abb002"></a>
![abb002](http://www.bilder-upload.eu/upload/aa1746-1447614050.png)   
[Abbildung 2: Anzahl parallel laufender Requests in verschiedenen Browsern](#abbildungsverzeichnis)    

Um die Anzahl an Requests zu verringern gibt es unter anderem folgende Möglichkeiten:

1.	**„Expires Header“  in HTTP verwenden**          
Der <a href="https://gtmetrix.com/add-expires-headers.html" target="_blank">Expires Header</a> im Browser entscheidet welche Dateien vom Server als Request angefordert  und welche aus dem Browser-Cache genommen werden. Er verhindert also das unnötige neu laden von Inhalten, wenn diese sowieso im Browser-Cache vorhanden sind. Der Expires Header setzt eine Zeit, wie lange bestimmte Dateien im Browser Cache als „aktuell“ bezeichnet und nicht noch einmal angefordert werden müssen. Somit kann unter Umständen die Anzahl an Requests drastisch verringert werden.   
2.	 **„CSS sprites“**       
Befinden sich auf einer Website besonders viele Bilder, lassen
sich mithilfe von <a href="http://www.w3schools.com/css/css_image_sprites.asp" target="_blank">CSS sprites</a> alle Bilder zu einem großen Bild zusammenfügen und einbinden. Mit Hilfe der CSS Einstellung lassen sich dann einzelne Bildausschnitte genau positionieren, so dass der Eindruck entsteht es wären viele einzelne Bilder vorhanden. Der Vorteil darin liegt aber das nur ein Bild zu Anfang geladen werden muss, und alle anderen somit sofort verfügbar sind was die Anzahl an HTTP-Requests drastisch reduzieren kann.   
3.	**Mehrere CSS und JavaScript Dateien zusammenfassen**       
Um nicht unnötig viele Dateien zu haben, die vom Server geladen werden müssen, kann man jeweils CSS  und JavaScript Dateien zusammenfassen. CSS und JavaScript wird sequentiell abgearbeitet, weswegen es ausreicht den Code jeweils in einer Datei „hintereinander zuhängen“.      

[*Startseite*](#top)


<a name="cssjavascript"></a>
#### 3.3 CSS und JavaScript optimieren


Im Code von CSS (Cascading Style Sheet) zum Verändern der Darstellung von Content, und JavaScript zur dynamischen Erweiterung von HTML, lassen sich ebenfalls einige Optimierungen vornehmen.

1.	**„Whitespaces“ minimieren**   
Um JavaScript und CSS Dateien zu verkleinern, können unnötige Leerzeichen (Whitespaces) entfernt werden. Das kann die Größe einer Website laut einer <a href="https://developer.yahoo.com/performance/rules.html#minify=" target="_blank">Untersuchung von Yahoo</a> um bis zu 21% reduzieren. In [Abbildung 3](#abb003) und [Abbildung 4](#abb004) sieht man wie ein CCS Teil mit und ohne Leerzeichen aussieht. Zusätzlich bringt das Entfernen von unnötigen Kommentaren im Code bei entsprechender Dateigröße einen hohen Einsparwert an Filegröße mit sich.  
<a name="abb003"></a>
  ![Abbildung 3](http://www.bilder-upload.eu/upload/42d5b5-1447757510.png)   
  [Abbildung 3: CSS mit Whitespaces](#abbildungsverzeichnis)   
<a name="abb004"></a>   
  ![Abildung 4](http://www.bilder-upload.eu/upload/d21be8-1447757559.png)   
  [Abbildung 4: CSS ohne Whitespaces](#abbildungsverzeichnis)  

 
2. **Auslagern**      
Da CSS und JavaScript einen sehr großen Teil des Quellcodes einer Website ausmachen, bietet es sich an diese auszulagern um den Ladevorgang zu verkürzen und redundanten Code zu vermeiden. Im Idealfall kann man alles in eine Datei schreiben und muss somit neben der HTML-Datei nur noch eine weitere laden. Wenn diese Datei auch noch im Browser-Cache gespeichert wird, spart man sich viel Zeit beim wiederholten Aufrufen der Website, da sich die Style Elemente in der Regel nur selten ändern und nicht erneut abgefragt werden müssen.  

3. **CSS an den Anfang - JavaScript an den Schluss**      
Um den Aufbau einer Website zu beschleunigen gibt es noch die Möglichkeit den Aufruf des CSS-Files an den Anfang eines HTML Dokuments zu setzen. Das stellt sicher das das Design zu Beginn geladen, und sich im Verlauf des HTML Dokuments stufenweise aufbaut. Ergänzend kann man dazu JavaScript Files an den Schluss setzen um den Seitenaufbau und das Abrufen von Daten und Files zu beschleunigen. Durch eine HTTP 1.1 Spezifikation blockieren Scripts den parallelen Download von Daten, dem mit dieser Möglichkeit aber vorgebeugt werden kann.      

[*Startseite*](#top)   


<a name="bilddateien"></a>
#### 3.4 Bilddateien optimieren


Da Bilder oft einen sehr großen Teil einer Website ausmachen, vor allem was ihre Dateigröße angeht, sollte man darauf achten diese zu optimieren. Große Bilddateien brauchen viel mehr Zeit zum Laden als einfacher Text, weswegen diese optimiert werden müssen.  
In [Abbildung 5](#abb005) sieht man die Größe einer durchschnittlichen Website, wobei mehr als 60% der Größe von Bilddateien bestimmt wird.
Nach einer Studie von <a href="http://httparchive.org/interesting.php#bytesperpage" target="_blank">httparchive (2014)</a> [(Abbildung 6)](#abb006) besitzt HTML und GIF die kleinste durchschnittliche Dateigröße. Die optimale Bilddatei ist aber PNG mit einer durchschnittlichen Größe von 18kB welche mit Optimierungstools wie <a href="http://optipng.sourceforge.net/" target="_blank">OptiPNG</a> oder <a href="http://advsys.net/ken/utils.htm" target="_blank">PNGOUT</a> noch für den Webgebrauch optimiert werden kann. Für hochauflösende Bilder sollte JPEG benutzt werden.


<a name="abb005"></a>
![Abbildung 5](http://chart.googleapis.com/chart?chs=400x225&cht=p&chco=007099&chd=t:1408,52,73,358,114,179,4&chds=0,1408&chdlp=b&chdl=total%202194%20kB&chl=Images+-+1408+kB%7CHTML+-+52+kB%7CStylesheets+-+73+kB%7CScripts+-+358+kB%7CFonts+-+114+kB%7CVideo+-+179+kB%7COther+-+4+kB&chma=|5&chtt=Average+Bytes+per+Page+by+Content+Type)   
[Abbildung 5: Verteilung auf einer durchschnittlichen Website](#abbildungsverzeichnis)

<a name="abb006"></a>   
![Abbildung 6](http://chart.googleapis.com/chart?chxl=1:|Video%7CCSS%7CJS%7CHTML%7CSVG%7CPNG%7CJPG%7CGIF&chdlp=b&chdl=average%20response%20size%20(kB&chxtc=0,6&chxs=0,676767,11.5,0,l|1,676767,11.5,1,lt,67676700&chxr=1,0,160|0,0,308&chxt=x,y&chbh=22&chs=640x310&cht=bhg&chco=3B356A&chds=0,308&chd=t:8,38,23,10,6,16,10,298&chm=N**+kB,676767,0,,12,,:4:&chma=|0,5&chtt=Average+Individual+Response+Size))   
[Abbildung 6: Größe von Dateien auf einer durchschnittlichen Website](#abbildungsverzeichnis) 

     
<a name="statehandling"></a>
#### 3.5 State Handling   
Das State Handling ist einer der wichtigsten Punkte für die Optimierung einer Webanwendung. Mit dem State Handling werden kleine Zustandsinformationen im Browser oder Server gespeichert um sie bei Bedarf abzurufen. Das geschieht in der Regel mit "Cookies" die elementare Informationen über den Benutzer und seine Session beinhalten. Speichert man solche Daten im Browser zwischen, spart man sich den ständigen Austausch zwischen Server und Client Man unterscheidet in 3 wesentlichen Kategorien:   

1. **Request State**    
Zustandsinformationen über laufende und kommende Requests.   
2. **Conversational State**   
Informationen, die über eine bestimmte Zeit zwischen gespeichert werden müssen, z.B. Formulardaten.   
3. **Session State**      
Wie der Name schon sagt werden hier Informationen über die aktuelle Sitzung gespeichert wie z.B. Benutzerdaten für einen aktuell laufenden Login auf einer Website.   


Solche Informationen sind zwar ungemein nützlich, sollten aber so klein wie möglich gehalten werden da sie Speicher im Browser beanspruchen. Dementsprechend sollten sie auch schnell wieder gelöscht werden wenn sie nicht mehr in Verwendung sind.      

[*Startseite*](#top)


<a name="wahrgenommen"></a>
## 4 Wahrgenommene Performance - "above the fold"


Viele Websites wollen mit interessantem Inhalt den Nutzer auf ihre Seite locken. Wenn dem Nutzer beim Betreten der Seite sofort ein bestimmter Abschnitt ins Auge springt, dann hat sich der Entwickler wahrscheinlich Gedanken über „above the fold“ gemacht. Der Begriff „above the fold“ stammt ursprünglich aus der Zeitungsindustrie, in der die Redakteure mit einem großen Bild oder einer interessanten Überschrift das Interesse des Käufers wecken will. Wer schon einmal an einem Kiosk die Zeitungsauslage gesehen hat, dem wird aufgefallen sein das diese Zeitung in der Mitte gefaltet sind, so dass nur der obere Teil zu sehen ist, in der meist das besagte Bild oder die Überschrift platziert ist. Man spricht also von einem „Eyecatcher“ über der Mittelfalte der Zeitung (engl. fold).
Diese Technik kommt auch vermehrt auf Websites zu tragen, da die Betreiber das gleiche Interesse haben wie der Redakteur der Zeitung, nämlich Nutzer für ihren Content zu begeistern.
Es ist umstritten ob diese Technik heutzutage noch anwendbar ist, da mit Zeiten von Smartphones und Tabletts die Bildschirmgröße stark variiert und somit nicht mehr gewährleistet werden kann das prägnante Inhalte auch tatsächlich innerhalb des initialen Viewports sichtbar sind. Außerdem ist mit der Zeit des scrollens und „wischen“ auf Smartphones die Wahrscheinlichkeit gestiegen das Nutzer gar nicht auf das Laden der Seite warten, sondern direkt anfangen zu scrollen und somit viel mehr Zeit unterhalb des „folds“ verbringen, was den eigentlichen Effekt von „above the fold“ zerstört. Deswegen sollte der obere Bereich auch nicht mit Informationen vollgestopft sein, sondern vielmehr das Interesse wecken um den Nutzer zum Bleiben zu überreden.

Eine Möglichkeit um dem Nutzer ein gezieltes Anzeigen von Informationen beim Betreten der Seite zu gewährleisten, ist diesen Bereich zu allererst anzeigen zu lassen, so dass diese möglichst sofort beim Betreten der Seite verfügbar ist. Den restlichen Content zögert man künstlich hinaus, damit der Nutzer anfangen kann den sichtbaren Bereich zu betrachten. Dies geschieht meistens indem man einen „critical above the fold style“ [(Abbildung 7)](#abb007) aus dem CSS isoliert und bestimmt, dass dieser als erstes ausgeführt werden soll, wenn ein Nutzer die Website betritt. So kann man sicherstellen das beim erstmaligen betreten der Website zuerst nur der obere, also der „above the fold“ Bereich, vom Browser gerendert wird, so dass sich der Nutzer mit diesem Content auseinandersetzen muss. Wichtige Inhalte werden also durch HTML/CSS vorzeitig geladen, ohne Rücksicht auf den eigentliche CSS Style.

<a name="abb007"></a>
![Abbildung 7](https://media-mediatemple.netdna-ssl.com/wp-content/uploads/2015/08/02-browser-opt-small.jpg)      
[Abbildung 7: Critical/Non-Critical CSS Bereich einer Website](#abbildungsverzeichnis)   

Im folgenden sehen Sie ein Beispiel, wie der "critical-part" in HTML implementiert werden kann:
<a name="abb008"></a>   

![Abbildung 8](http://www.bilder-upload.eu/upload/a2e527-1447756570.png)   
[Abbildung 8: Mögliche implementierung von "critical-css" in HTML](#abbildungsverzeichnis)   

[*Startseite*](#top)


<a name="user"></a>
## 5 Was kann der User tun?


Alle angesprochenen Optimierungsmöglichkeiten sind für die Entwickler einer Webanwendung wahrscheinlich sehr interessant, für den einfachen User der sich tagtäglich mit langsamen Websites auseinandersetzen muss sind sie allerdings weniger interessant und hilfreich. Trotzdem gibt es auch für den End User einige Möglichkeiten die er ausprobieren kann, wenn seine Lieblingswebsite des Öfteren lange Ladezeiten aufweist.   

1. **Ersthilfe**   
Das erste was der User überprüfen sollte ist, ob die Version des Browsers auf dem aktuellsten Stand ist, gegebenenfalls müssen Updates installiert werden. Das gleiche gilt für die Netzwerktreiber.
Ist die Internetverbindung im Allgemeinen langsam, hilft oft auch ein Router Neustart wahre Wunder. Hat man vom Anbieter aus sowieso schon eine langsame Internetgeschwindigkeit, sollte man einen Netzwechsel oder ein Upgrade in Erwägung ziehen. Ist die Internetgeschwindigkeit von Haus aus langsam, oder es benutzen viele Personen gleichzeitig dasselbe Netz, hilft auch der beste Optimierungsversuch nicht.
Trifft das alles nicht zu, sollte man sich den Browser genauer anschauen.   

2. **Google Chrome – Inkognito-Fenster**   
Chrome bietet die Möglichkeit ein neues Inkognito-Fenster zu erstellen in dem alle Erweiterungen und der Browsercache ignoriert werden. Öffnet man jetzt eine neue Website und diese wird gewohnt schnell geladen, dann liegt das Problem meist an unnötigen Datenmüll im Browser der die Verbindung verlangsamt.   

3. **Datenmüll entfernen**   
Im Cache des Browsers kann sich bei langer Nutzung unnötiger Datenmüll angesammelt haben, der nicht mehr gebraucht wird. Programme wie <a href="https://www.piriform.com/ccleaner" target="_blank">CCleaner</a> bieten eine gute Möglichkeit den Browsercache und weiteren Datenmüll zu entfernen. Viele Browser unterstützen auch die Möglichkeit beim Beenden des Browsers den Cache oder die Chronik automatisch zu löschen.

4. **Unnötige Addons/Plugins entfernen**   
Die meisten Browser unterstützen die Möglichkeit Plugins oder Addons (Browser spezifisch) zu installieren. Das geschieht oft unbewusst bei dem Betreten von Websites die diese Addons  voraussetzen. Um unnötige Plugins und Addons aus dem Browser zu löschen findet man in der Regel unter „Einstellungen“ -> „Erweiterungen“/“Addons“/“Plugins“ alle installierten und aktivierten Erweiterungen des Browsers aufgelistet und kann sie manuell löschen.

5. **Prozess-Priorität erhöhen**   
Im Task-Manager von Windows kann man einzelnen Prozessen eine höhere Priorität zuweisen, so dass ihnen mehr Ressourcen zugewiesen werden und somit in der Regel schneller arbeiten. Rechtsklick auf den Prozess des Browsers und dann „Priorität festlegen“ -> „Hoch“ oder „Echtzeit“ gibt das gewünschte Ergebnis.

6. **Aktivierten Proxy deaktivieren**   
Falls die Verbindung langsam sein sollte, kann es eventuell daran liegen, dass sie über einen externen Proxy-Server läuft. Damit wird die Verbindung über den Browser erst über einen weiteren externen Server umgeleitet, bevor sie am Ziel-Host ankommt. Unter „Einstellungen“ findet man in der Regel eine Netzwerk bzw. Proxy Einstellung, in der man gegebenenfalls eingestellte Umleitungen aufheben kann.

7. **Hardware-Beschleunigung aktivieren**   
Firefox und Google Chrome bieten die Möglichkeit neben der CPU auch die Grafikkarte zur Bearbeitung im Browser hinzuzuziehen. Unter „Einstellungen“ ->“Erweitert“(Firefox) / „Erweiterte Einstellungen anzeigen“(Chrome) kann man die Hardware-Beschleunigung aktivieren (falls verfügbar).

8. **"Malware"**  
Ein weiterer Grund warum der Browser an Geschwindigkeit einbüßt, ist eventuelle Schadsoftware auf dem Computer, sogenannte <a href="https://de.wikipedia.org/wiki/Schadprogramm" target="_blank">"Malware"</a>. Am einfachsten ist eine Systemüberprüfung mit einem Antiviren/Antimalware-Programm, um diese Möglichkeit auszuschließen. Kostenlose Möglichkeiten sind unter anderem <a href="http://www.chip.de/downloads/SpyBot-Search-Destroy_13001443.html" target="_blank">"SpyBot"</a>, <a href="http://www.chip.de/downloads/Ad-Aware-Free_13000824.html" target="_blank">"Ad-Aware Free Antivirus+"</a> oder <a href="http://www.chip.de/downloads/AntiVir-2015-Avira-Free-Antivirus_12998486.html" target="_blank">"AntiVir 2015"</a>.

9. **Browser reset**   
Wenn gar nichts mehr geht, und alle Optimierungsmöglichkeiten ausgeschöpft sind, dann hilft oft nur noch den Browser auf Werkeinstellungen zurückzusetzen. Um den Reset ohne Datenverlust zu abzuschließen, findet sich
<a href="http://artikel.de.softonic.com/langsamer-browser-einfach-zurucksetzen-ohne-datenverluste" target="_blank">hier</a>
ein Artikel wie bei den unterschiedlichen Browsern vorgegangen werden muss.




[*Startseite*](#top)


<a name="fazit"></a>
## 6 Fazit

Performance ist ein sehr wichtiges Thema, vorallem in so einer schnelllebigen Zeit wie der des Internets. Mit dem weltweiten Netzausbau und der stetigen Verbesserung des Internets, sind die Entwickler von Webanwendungen gezwungen auf die Wünsche des Users einzugehen, und Webanwendungen stetig zu optimieren. Dabei spielt die Geschwindigkeit, wie in so vielen Bereichen des Lebens eine große und tragende Rolle. Ist man Entwickler einer solchen Webanwendung sollte man schon bei der Planung die spätere Performance einschätzen und berechnen können. Denn behebt man bei der Konzeption und Entwicklung schon Fehler die die Performance beeinflussen können, spart man sich später viel Zeit und Mühe etwaige Fehler auszumerzen Als Nutzer einer solchen Webanwendung ist man aber auch nicht vollkommen hilflos und muss zusehen, wie der Browser mit der Zeit immer langsamer wird. Es gibt zahlreiche Tools und Anleitungen im Internet wie man die Performance auf Seiten des Nutzers verbessern kann. Grundsätzlich kann man sagen: Schlechte Performance kostet Zeit, und Zeit ist Geld! Sowohl für den Nutzer als auch für die Betreiber einer Webanwendung.

[*Startseite*](#top)


<a name="quellen"></a>
## 7 Quellen   

* <a href="https://dpunkt.de/leseproben/3884/4_Einfuehrung%20in%20die%20Performance-Optimierung.pdf" target="_blank">https://dpunkt.de/leseproben/3884/4_Einfuehrung%20in%20die%20Performance-Optimierung.pdf</a>   
* <a href="http://www.informatik-aktuell.de/entwicklung/methoden/performance-optimierung-bei-java-webanwendungen.html" target="_blank">http://www.informatik-aktuell.de/entwicklung/methoden/performance-optimierung-bei-java-webanwendungen.html</a>   
* <a href="http://www.pc-erfahrung.de/nebenrubriken/sonstiges/webdesignwebentwicklung/page-speed-optimieren.html" target="_blank">http://www.pc-erfahrung.de/nebenrubriken/sonstiges/webdesignwebentwicklung/page-speed-optimieren.html</a>   
* <a href="https://de.onpage.org/blog/tipps-fur-bessere-website-performance" target="_blank">https://de.onpage.org/blog/tipps-fur-bessere-website-performance</a>   
* <a href="http://www.seitenreport.de/kb/-/grundlagen-der-website-performance-1-requests.html" target="_blank">http://www.seitenreport.de/kb/-/grundlagen-der-website-performance-1-requests.html</a>   
* <a href="https://gtmetrix.com/add-expires-headers.html" target="_blank">https://gtmetrix.com/add-expires-headers.html</a>   
* <a href="http://httparchive.org/interesting.php#bytesperpage" target="_blank">http://httparchive.org/interesting.php#bytesperpage</a>   
* <a href="http://www.admin-wissen.de/tutorials/php_tutorial/fortgeschrittene/performanceanalyse_und_optimierung/performance_messen.html" target="_blank">http://www.admin-wissen.de/tutorials/php_tutorial/fortgeschrittene/performanceanalyse_und_optimierung/performance_messen.html</a>   
* <a href="http://grinder.sourceforge.net/" target="_blank">http://grinder.sourceforge.net/</a>   
* <a href="http://loaduiweb.org/" target="_blank">http://loaduiweb.org/</a>   
* <a href="http://jmeter.apache.org/index.html" target="_blank">http://jmeter.apache.org/index.html</a>   
* <a href="http://www.w3schools.com/css/css_image_sprites.asp" target="_blank">http://www.w3schools.com/css/css_image_sprites.asp</a>   
* <a href="http://alistapart.com/article/sprites" target="_blank">http://alistapart.com/article/sprites</a>   
* <a href="https://www.google.com/intl/de_de/analytics/" target="_blank">https://www.google.com/intl/de_de/analytics/</a>   
* <a href="https://de.wikipedia.org/wiki/Cache" target="_blank">https://de.wikipedia.org/wiki/Cache</a>   
* <a href="https://developer.yahoo.com/performance/rules.html#minify=" target="_blank">https://developer.yahoo.com/performance/rules.html#minify=</a>   
* <a href="https://de.onpage.org/blog/above-the-fold-webseiten-richtig-aufbauen" target="_blank">https://de.onpage.org/blog/above-the-fold-webseiten-richtig-aufbauen</a>   
* <a href="http://t3n.de/news/above-the-fold-antwort-wichtigste-frage-608789/" target="_blank">http://t3n.de/news/above-the-fold-antwort-wichtigste-frage-608789/</a>   
* <a href="https://www.piriform.com/ccleaner" target="_blank">https://www.piriform.com/ccleaner</a>
* <a href="https://de.wikipedia.org/wiki/Schadprogramm" target="_blank">https://de.wikipedia.org/wiki/Schadprogramm</a>   
* <a href="http://www.chip.de/downloads/SpyBot-Search-Destroy_13001443.html" target="_blank">http://www.chip.de/downloads/SpyBot-Search-Destroy_13001443.html</a>   
* <a href="http://www.chip.de/downloads/Ad-Aware-Free_13000824.html" target="_blank">http://www.chip.de/downloads/Ad-Aware-Free_13000824.html</a>   
* <a href="http://www.chip.de/downloads/AntiVir-2015-Avira-Free-Antivirus_12998486.html" target="_blank">http://www.chip.de/downloads/AntiVir-2015-Avira-Free-Antivirus_12998486.html</a>   
* <a href="http://artikel.de.softonic.com/langsamer-browser-einfach-zurucksetzen-ohne-datenverluste" target="_blank">http://artikel.de.softonic.com/langsamer-browser-einfach-zurucksetzen-ohne-datenverluste</a>   


[*Startseite*](#top)  


<a name="abbildungsverzeichnis"></a>
## 8 Abbildungsverzeichnis


* [*Abbildung 1*](#abb001): <a href="https://www.codecentric.de/kompetenzen/publikationen/performance-im-umfeld-von-webanwendungen/" target="_blank">https://www.codecentric.de</a>     
* [*Abbildung 2*](#abb002): <a href="http://www.seitenreport.de/kb/-/grundlagen-der-website-performance-1-requests.html" target="_blank">http://www.seitenreport.de</a>  
* [*Abbildung 3*](#abb003): vom Autor erstellt   
* [*Abbildung 4*](#abb004): vom Autor erstellt  
* [*Abbildung 5*](#abb005): <a href="http://httparchive.org/interesting.php#bytesperpage" target="_blank">http://httparchive.org</a>   
* [*Abbildung 6*](#abb006): <a href="http://httparchive.org/interesting.php#bytesperpage" target="_blank">http://httparchive.org</a>        
* [*Abbildung 7*](#abb007): <a href="http://www.smashingmagazine.com/2015/08/understanding-critical-css/" target="_blank">http://www.smashingmagazine.com</a>         
* [*Abbildung 8*](#abb008): vom Autor erstellt   

[*Startseite*](#top)
