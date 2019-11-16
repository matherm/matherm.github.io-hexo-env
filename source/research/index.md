---
title: Research Projects
date: 2018-09-16 11:23:32
---

# Research projects I'm working on 
**2019-2022 | Photonics BW MultiSenseLakePerceptor: Optisches Multisensorsystem für autonome Anwendungen auf Binnengewässern**
<img src="/images/lakeperceptor.png", width=300>
Im Rahmen des Projekts soll die Problemstellung mit optischen Sensoren verbunden mit Lidar gelöst werden. Durch Ver­netzung unterschiedlicher Sensortypen wird ein geeignetes Abbild der komplexen dynamischen 3D-Szene erstellt (siehe Abbildung 2) und dieses dann Tracking- und Klassi­fikationsalgorithmen zur Verfügung gestellt. Die sensorspezifischen 3D-Punktwolken sind zu diesem Zeitpunkt weder zueinander registriert noch fusioniert. Zur Schätzung der einzelnen Tiefenkarten und Objektlisten mittels Machine-Learning, wird innerhalb des Projekts eine neuartige Deep-Learning Ar­chitektur entwickelt. Im Vergleich zu heutigen Convolutional Neural Networks muss diese mit den für 3D-Punktwolken typischen Messpunkten ohne feste Nachbarschaftsbezie­hungen zurechtkommen. [>>Project website](http://www.ios.htwg-konstanz.de/node/605)

**2017-2021 | BMBF Multifunktional-skalierbare generische InlineInspektion für flexible Fertigungsprozesse in vernetzten Produktionsanlagen**
<img src="/images/multiflex.png">
Erstmalig sollen dabei bei der Bewertung nicht nur rein technische Aspekte, sondern auch von außen kommende Informationen (z. B. wahrnehmungsmotivierte Qualitätsbewertungen eines Menschen) in das Modell mit eingebunden werden, wofür die HTWG Konstanz verantwortlich zeichnet. Damit soll – einzigartig in der Inline-Inspektionstechnik – dem Aspekt Rechnung getragen werden, dass bei der Wahrnehmung von Defekten oft enorme Diskrepanzen in der Bewertung durch Mensch und Maschine bestehen, insbesondere für farbige texturierte 3D-Oberflächen. Heute kommt es nicht selten vor, dass Defekte auf Basis des menschlichen Eindrucks durchaus toleriert würden, während klassische maschinelle Inspektionsmodelle zur Fehlermeldung führen und somit zur Überklassifikation. [>>Project website](https://www.photonikforschung.de/projekte/photonische-prozessketten/projekt/multiflexinspect.html)


# Selected special topics 
**2019 | Scene Reconstruction with HD-Streams**
<img src="/images/henning.png">
<img src="/images/henning2.png">
Team: Matthias Hermann, Henning Krause, Kevin Deggelmann, Benjamin Bäumler Hendrik Aufderstroth, Patrick Fiur
Unser Projekt befasst sich mit der automatisierten Rekonstruktion existierender Hausfassaden. Ziel war es, ein 3D-Modell zu erzeugen, das genau genug ist, um darin Vermessungen durchzufuhren, wie sie von einem Architekturbüro oder einem Fassadenbauer benotigt werden, z.B. die Fläche der Fassade ohne Fenster oder der Abstand der Fenster untereinander. Im Laufe des Projekts trafen wir auf einige Hindernisse, von denen sich nicht alle im Rahmen des Projekts losen ließen. Wir präasentieren den Prototyp einer Software, die aus monokularen Videodaten ein darin abgebildetes Objekt dreidimensional als Punktwolke rekonstruiert. Als Sensor setzen wir ausschließlich die Kamera eines handelsublichen ferngesteuerten Quadrokopters ein.


**2019 | Hardware acceleration of Neural Networks using FPGAs** 
<img src="/images/fpga.png">
Team: Matthias Hermann, Marcel Arpogaus, Daniel Dold, Dennis Restle
The purpose of this project is to analyze the possibilities of model compression to enable
the execution of Neural Networks in real time computer Vision and Object recognition
tasks on FPGAs. The biggest challenge is the transition of the model from a floating point training
environment to pure integer arithmetics. We expose the insights of training, quantizing and transferring the resulting model onto the embedded hardware using commonly know techniques. Additional effort was put into implementing a custom FPGA architecture for CNNs, which we compared to a proprietary closed-source solution.


**2019 | Analysis of point cloud convolutions for edge detection on point clouds** 
<img src="/images/joey.png">
Team: Matthias Hermann, Joey Rieg
Edge detection is essential in a variety of fields, escpecially in autonomous systems, where feature-edges define the shape of the environment.
Algorithms to detect edges are also applied in other fields such as medical image processing to find anomalies in the human body. The main data edge detection is applied to are images. With the development of 3-dimensional sensor such as light detection and ranging (LiDAR) unstructured
data such as point clouds are easier to obtain and are already used in before mentioned autonomous systems with deep learning algorithms to solve tasks on
object detection scene segmentation


**2019 | Feasibility of reinforcement learning for point cloud preprocessing**
<img src="/images/jonas.png">
Team: Matthias Hermann, Jonas Fleischer
Machine learning techniques have already been successfully applied when working with point clouds. Examples of this include, among other things, robotic grasping,
segmentation, classification, and learning knot placement for B-spline curves.However, the point cloud preprocessing is often performed with handcrafted
heuristics. This thesis explores the viability of point cloud preprocessing using reinforcement learning. Specifically, sequencing, selection, and segmentation tasks
are evaluated. For this purpose, the performance of five common reinforcement learning algorithms is measured. 


**2019 | Vergleich verschiedener Farbräume zur novelty detection mit Neuronalen Netzen**
<img src="/images/tolga.png">
Team: Matthias Hermann, Tolga Cetingoez, Tobias Birkle 
Diese Arbeit beschäftigt sich mit Anomalieerkennung in verschiedenen Farbr¨aumen. Dazu wird ein neuronales Netz mit fehlerfreien Daten trainiert. Fehlerhafte Daten soll das Netzwerk dadurch aussortieren können. Es wurden die Farbr¨aume RGB und HSV sowie das Farbmodell YUV untersucht. Es wurde ein Farbintervall erstellt mithilfe von
Dropout. Alle Werte die nicht innerhalb dieses Farbintervalls liegen, sind Anomalien. Hierbei wurden gute Ergebnisse fur RGB und HSV erzielt


**2019 | Anomaliedetektion an digital gedruckten Dekoren mit Hilfe von künstlichen neuronalen Netzen**
<img src="/images/semih.png">
Team: Matthias Hermann, Semih Demir, Tobias Birkle
Künstliche neuronale Netze werden in der Industrie immer beliebter, da sie Aufgaben wie Spracherkennung, Trendprognosen sowie Bildverarbeitung vor allem bei großen
Datenmengen deutlich besser als Menschen bewältigen können. Ein bereits trainiertes Netz, kann im Gegensatz zum Menschen, Millionen Datensätze in wenigen Stunden
verarbeiten. Dies kann z. B. die Auswertung von MRT Aufnahmen in der Medizin oder Material- bzw. Oberflächeninspektion in der Produktion sein.


**2019 | Modelling digital printing transformation with neural networks**
<img src="/images/simon.png">
Team: Matthias Hermann, Simon Christofzik
Insbesondere im industriellen Bereich rückt der Einsatz von neuronalen Netzen immer mehr in den Vordergrund. Das Inspizieren von Produkten wie z.B. Parkettböden übernehmen Computer, welche darauf ausgelegt sind Fehler am Produkt zu erkennen und diese aussortieren. Das Trainieren eines neuronalen Netzwerk auf solche Anwendungen benötigt eine grosse Anzahl an Daten, deren Beschaffung oft eine mühsame Aufgabe darstellt. Des weiteren müssen die Daten gewissen Anforderungen entsprechen. Um dies zu erreichen kann es erforderlich sein, ein grossen Satz an Daten von Hand durch zugehen und fehlerhafte Daten aussortieren. Im Falle der Parkettböden müssten zuerst Daten erhoben werden, indem Referenzböden gedruckt werden. Diese müssen auf Fehler überprüft werden und können dann in das Datenset aufgenommen werden. Diesen Prozess zu automatisieren, indem synthetische Parkettböden erzeugt werden ist eine erstrebenswerte Aufgabe, die die Datenerhebung wesentlich vereinfacht.


**2018 | Geodesic Distances based on Heat Method and Fast Marching Method**
<img src="/images/daniel.png">
Team: Matthias Hermann, Daniel Kuhn
This work presents the comparison of the relatively new Heat Method and the well-known and frequently applied Fast Marching Method. Both methods can be used for many computational problems such as geodesic calculations and path extractions. Furthermore, this article proves the results of the research work carried out
by Keenan Crane, Clarisse Weischedel, and Max Wardetzky for the Heat Method. While being an order of magnitude faster than the Fast Marching Method, the Heat Method achieves almost the same error rate.


**2018 | Signal separation: Comparison between neural networks and transformational codes**
<img src="/images/ica.gif">
Team: Matthias Hermann, Thomas Gnädig, Michael Grunwald
In dieser Arbeoit wird das Verhalten künstlicher neuronaler Netze mit dem der Independent Component Analysis bei der Signaltrennung verglichen. Neuronale Netze zeigen ein großes Potential zur Lösung vieler Probleme in der modernen Informatik. Da aber die Vorgehensweise zum Erreichen dieser Lösungen nicht immer deutlich ist, wird diese hier mit der Independent Component Analysis verglichen.


