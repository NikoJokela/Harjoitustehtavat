ohjelmalista = {}
sali_1 = [x for x in range(1,19)]
varaus_1 = []                       #EI TOIMI VARAUKSET
sali_2 = [x for x in range(1,41)]
varaus_2 = []
sali_3 = [x for x in range(1,33)]
varaus_3 = []

def tallenna_elokuva(ohjelmalista:dict, elokuva:str, kellonaika:str, sali:int):
    ohjelmalista[elokuva] = (kellonaika, sali)
    with open("ohjelmalista.txt","a") as ol:
        ol.write(f"Elokuva: {elokuva}, kellonaika: {kellonaika}, sali: {sali}" "\n")
    
def onko_elokuva(ohjelmalista:dict, elokuva:str) -> bool:
    if elokuva in ohjelmalista:
        return True
    else:
        return False
      
def poista_elokuva(elokuva:str, kellonaika:str, sali:int) -> bool: #poistaa tällä hetkellä monta elokuvaa, jos kellonaika on sama!  
    #del ohjelmalista[elokuva]
    
    with open("ohjelmalista.txt","r") as ol:
        rivit = ol.readlines()
    with open("ohjelmalista.txt","w") as ol:
            for rivi in rivit:
                if sali and kellonaika and elokuva not in rivi:
                    ol.write(rivi)
    return True

def tulosta_ohjelmalista():
    #if len(ohjelmalista) > 0:
    #   avain = list(ohjelmalista.keys())
     #   arvot = list(ohjelmalista.values())
     #   print("Ohjelmalista: ")
     #   for i in range(len(avain)):
     #       print(f"{avain[i]}, Kello: {arvot[i][0]}, Sali: {arvot[i][1]} ")
    with open("ohjelmalista.txt") as ol:
        sisalto = ol.read()
        print(sisalto)

def varaus_tietokantaan(elokuva:str, sali:int, paikka:int):
    with open("tietokanta.txt","a") as tk:
        tk.write(f"Varattu liput elokuvaan {elokuva} salissa {sali} istumapaikalta {paikka}" "\n")

print("Tervetuloa elokuvateatterin varausjärjestelmään.\nValitse käyttötarkoitus.")
print("1: Ylläpitäjä")
print("2: Asiakas")
print("0: Sulje ohjelma")
while True:
    try:
        valinta = int(input("Valinta: "))
        if valinta == 0 or 1 or 2:
            break
    except ValueError:
        print("Syöte pitää olla luku, ei kirjain! Vain 1, 2 tai 0!")

while valinta != 0:
    if valinta == 1:
        salasana = input("Anna salasana: ")
        if salasana == "salasana":
            
            print("----------------------------------------")
            print("Elokuvateatterin varausjärjestelmä")
            print("Valitse:")
            print("1: Lisää elokuva ohjelmistoon")
            print("2: Poista elokuva ohjelmistosta")
            print("3: Listaa ohjelmisto")
            print("4: Selaa varauksia")
            print("0: Poistu")
            print("----------------------------------------")
            while True:
                try:
                    valinta = int(input("Valinta: "))
                    if valinta == 0 or 1 or 2 or 3 or 4:
                        break
                except ValueError:
                    print("Syöte pitää olla luku, ei kirjain! Vain 0, 1, 2, 3 tai 4")

            while valinta != 0:     #Ylläpitäjän käyttöliittymä

                if valinta == 1:
                    elokuva = input("Elokuvan nimi: ")
                    kellonaika = input("Lisää kellonaika: ")
                    sali = int(input("Salin numero: "))
                    tallenna_elokuva(ohjelmalista, elokuva, kellonaika, sali)
                
                elif valinta == 2:
                    elokuva = input("Anna elokuvan nimi: ")
                    kellonaika = input("Anna kellonaika: ")
                    sali = input("Anna salin numero: ")
                    poista_elokuva(elokuva, kellonaika, sali)
                    print(f"Elokuva {elokuva} kello {kellonaika} salista {sali} poistettu.")
                
                elif valinta == 3:
                    tulosta_ohjelmalista()
                
                elif valinta == 4:
                    with open("tietokanta.txt","r") as tk:
                        sisalto = tk.read()
                        print(sisalto)

                print("----------------------------------------")
                print("Elokuvateatterin varausjärjestelmä")
                print("Valitse:")
                print("1: Lisää elokuva ohjelmistoon")
                print("2: Poista elokuva ohjelmistosta")
                print("3: Listaa ohjelmisto")
                print("4: Selaa varauksia")
                print("0: Poistu")
                print("----------------------------------------")
                
                while True:
                    try:
                        valinta = int(input("Valinta: "))
                        if valinta == 0 or 1 or 2 or 3 or 4:
                            break
                    except ValueError:
                        print("Syöte pitää olla luku, ei kirjain! Vain 0, 1, 2, 3 tai 4.")
        else: 
            print("Väärä salasana!")     

    elif valinta == 2:
        print("----------------------------------------")
        print("Elokuvateatterin varausjärjestelmä")
        print("Valitse:")
        print("1: Listaa ohjelmisto")
        print("2: Varaa paikka")
        print("0: Poistu")
        print("----------------------------------------")
        while True:
            try:
                valinta = int(input("Valinta: "))
                if valinta == 0 or 1 or 2:
                    break
            except ValueError:
                print("Syöte pitää olla luku, ei kirjain! Vain 1, 2 tai 0.")

        while valinta != 0: #Asiakkaan käyttöliittymä
            if valinta == 1:
                tulosta_ohjelmalista()
               
            elif valinta == 2:
                
                while True:
                    elokuva = input("Valitse elokuva, 0: palaa takaisin: ")
                    if onko_elokuva(ohjelmalista, elokuva):
                        break
                    if elokuva == "0":
                        break
                    if not onko_elokuva(ohjelmalista, elokuva):
                        print("Elokuvaa ei ole ohjelmistossa!")

                while True:
                    try:
                        sali = int(input("Valitse sali: "))
                        if sali == 1 or 2 or 3:
                            break
                    except ValueError:
                        print("Salin numero pitää olla 1, 2 tai 3.")
 
                if sali == 1:
                    print("___________________")
                    print("|13|14|15|16|17|18|")
                    print("|07|08|09|10|11|12|")
                    print("|01|02|03|04|05|06|")
                    print("|_____Screen______|")
                    print("Varatut paikat: ", varaus_1)

                    while True:
                        try:
                            paikka = int(input("Valitse istumapaikka (esim 1, 9, 13): "))
                            if type(paikka) == int:
                                break
                        except ValueError:
                            print("Paikka pitää antaa numerona!")

                    if paikka > len(sali_1) or paikka < 1:
                        print("Paikkaa ei ole! Katso salin istumapaikat ja yritä uudelleen.")
                    if paikka in varaus_1:
                        print("Paikka on jo varattu!")
                    if len(varaus_1) >= 18:
                        print("Sali on täynnä!")
                    if paikka in sali_1 and paikka not in varaus_1 and len(varaus_1) < 18:
                        print("Varattu paikka", paikka)
                        varaus_1.append(paikka)
                        varaus_tietokantaan(elokuva, sali, paikka)

                                 
                elif sali == 2:
                    print("_______________________________")
                    print("|31|32|33|34|35|36|37|38|39|40|")
                    print("|21|22|23|24|25|26|27|28|29|30|")
                    print("|11|12|13|14|15|16|17|18|19|20|")
                    print("|01|02|03|04|05|06|07|08|09|10|")
                    print("|___________Screen____________|")
                    print("Varatut paikat: ", varaus_2)

                    while True:
                        try:
                            paikka = int(input("Valitse istumapaikka (esim 1, 9, 13): "))
                            if type(paikka) == int:
                                break
                        except ValueError:
                            print("Paikka pitää antaa numerona!")

                    if paikka > len(sali_2) or paikka < 1:
                        print("Paikkaa ei ole! Katso salin istumapaikat ja yritä uudelleen.")
                    if paikka in varaus_2:
                        print("Paikka on jo varattu!")
                    if len(varaus_2) >= 40:
                        print("Sali on täynnä!")
                    if paikka in sali_2 and paikka not in varaus_2 and len(varaus_2) < 40:
                        print("Varattu paikka", paikka)
                        varaus_2.append(paikka)
                        varaus_tietokantaan(elokuva, sali, paikka)

                elif sali == 3:
                    print("_________________________")
                    print("|25|26|27|28|29|30|31|32|")
                    print("|17|18|19|20|21|22|23|24|")
                    print("|09|10|11|12|13|14|15|16|")
                    print("|01|02|03|04|05|06|07|08|")
                    print("|________Screen_________|")
                    print("Varatut paikat: ", varaus_2)

                    while True:
                        try:
                            paikka = int(input("Valitse istumapaikka (esim 1, 9, 13): "))
                            if type(paikka) == int:
                                break
                        except ValueError:
                            print("Paikka pitää antaa numerona!")

                    if paikka > len(sali_3) or paikka < 1:
                        print("Paikkaa ei ole! Katso salin istumapaikat ja yritä uudelleen.")
                    if paikka in varaus_3:
                        print("Paikka on jo varattu!")
                    if len(varaus_3) >= 32:
                        print("Sali on täynnä!")
                    if paikka in sali_3 and paikka not in varaus_3 and len(varaus_3) < 32:
                        print("Varattu paikka", paikka)
                        varaus_3.append(paikka)
                        varaus_tietokantaan(elokuva, sali, paikka)
                
            print("----------------------------------------")
            print("Elokuvateatterin varausjärjestelmä")
            print("Valitse:")
            print("1: Listaa ohjelmisto")
            print("2: Varaa paikka")
            print("0: Poistu")
            print("----------------------------------------")
            while True:
                try:
                    valinta = int(input("Valinta: "))
                    if valinta == 0 or 1 or 2:
                        break
                except ValueError:
                    print("Syöte pitää olla luku, ei kirjain! Vain 1, 2 tai 0!") 

    print("Tervetuloa elokuvateatterin varausjärjestelmään.\nValitse käyttötarkoitus.")
    print("1: Ylläpitäjä")
    print("2: Asiakas")
    print("0: Sulje ohjelma")
    while True:
        try:
            valinta = int(input("Valinta: "))
            if valinta == 0 or 1 or 2:
                break
        except ValueError:
            print("Syöte pitää olla luku, ei kirjain! Vain 1, 2 tai 0!")

            

        
