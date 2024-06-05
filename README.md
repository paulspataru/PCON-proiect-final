## Generator de muzica algoritmica inspirat de atmospheric drum and bass 

Programul este realizat utilizand pure data vanilla fara nicio biblioteca externa. Acesta genereaza secvente pe 3 trackuri, unul pentru tobe, in care se citeste un sample si bpm ul acestuia care este folosit pt celelalte trackuri, si apoi
doua trackuri in care muzica este sintetizata pentru bass, respectiv synth, iar patternul de note este generat prin lanturi markov. Sunt foarte multi paramatrii care pot fi ajustati pentru schimbarea sunetului, unii sunt destul de intuitivi,
insa o mare parte din ei, mai ales variabilele din randomiserele sintetizatoarelor necesita putina rabdare...

Folosind Plugdata, track-urile pot fi incarcate in Reaper. Pentru aceasta a fost nevoie de OSC. 

## Instalare
Toate fisierele trebuie sa fie impreuna in acelasi folder la fel cum sunt downloadate din repo.
Pentru incarcarea in Reaper trebuie instalat plugdata si incarcat in track plugdata-fx care permite alegerea oricarui patch de tip .pd pe post de vst. "drumReaper.pd" este patch-ul nu doar genereaza tobele, dar si secventele si trimite resul parametrilor
catre "bassReaper.pd" si "synthReaper.pd".

## Utilizare
Acesta este patch-ul principal - "console.pd", folosit pe post de controler pentru tot programul:
![image](https://github.com/paulspataru/PCON-proiect-final/assets/168900477/8a364a85-7b57-4c66-8626-caceacc1965f)

Zona din stanga citeste sample-urile de tobe si extrage bpm-ul, dupa care genreaza evenimente de bang pentru per x baruri care sunt folosite pentru sincronizare.

"markov2" e un patch care alege secvente pe baza unor probabilitati markov. Este alcatuit randomisere ponderate numite "w5random" si un multiplexor cu 5 canale. Patch-ul are un fel de feedback loop, deci are nevoie de o intarziere. Pe aceeasi idee sunt
si patchurile care genereaza patternurile de note, doar ca ele lucreaza cu 4 stari. 
![image](https://github.com/paulspataru/PCON-proiect-final/assets/168900477/7151886a-3969-4b28-89cb-7be3820217b1)

In urmatoarea zona se pot alege valorile pt minim si maxim de durata a secventelor. Ele se aleg in secunde si sunt convertite in beaturi. 

Zona din dreapta are sliderele de volume pe fiecare canal si patchurile de unde vine sunetul pt synth si bass.

Pentru Reaper, drumReaper este joaca rolul lui console.pd in mare parte.

## Setari default
In drum track este ales pe baza unor ponderi un sample dintre cele 8 incarcate in folder. Sample-ul este taiat in 3 si se construieste un loop din alegerea random a unui slice dupa incehierea fiecaruia. Din motive de gusturi personale am inclus si un
obiect de clipping pentru putina distorsie.
![image](https://github.com/paulspataru/PCON-proiect-final/assets/168900477/74ce09b4-fc2a-4de3-8383-1eabd31d9a44)

Basul este sintetizat cu un sinus de joasa frecventa comprimat dupa legea miu si taiat asimetric pentru mai multa saturatie. La fiecare genereare de pattern se alege si o anvelopa random pentru nota - sau se intrerupe nota pentru pozitiile 2/5/6/7 
![image](https://github.com/paulspataru/PCON-proiect-final/assets/168900477/718a0bf7-5677-4fa1-b334-9583a905f4cc)

Synth-ul este sintetizat cu zgomot alb tracut prin fitre trece banda pe primele 10 armocici cu Q foarte mare, si la fiecare schimbare de set armonicele sunt randomizate astfel incat sa se prioritizeze armonicele pare si joase.
De asemenea sunt generate corzi decate 4, decalate cu 2 semitonuri, ale caror nivele sunt de asemena randomizate pe acelasi principiu. In mod default, anvelopa este foarte mare dar si velocitatea este setata la 0.7.
![image](https://github.com/paulspataru/PCON-proiect-final/assets/168900477/8f609f76-4c43-4bf8-af34-20e55a805625)

## Istoric

Final aprilie 2024:
- drum track-ul si randomiserele pentru ponderate

Mijlocul lui mai 2024:
- prima varianta de bas track si primul sintetizator

Final mai 2024:
- refacut sintetizator
- patch-ul console.pd pt control si UI
- patchurile pentru reaper

Ultimele retusuri 3-5 inuie:
- adaugat optinuea pentru fara nota pe bass

## Link-uri
Inspiratie principala:
[...](https://www.youtube.com/watch?v=OwkacnSUn10&t=89s)



