import json
ohjelmalista = {"elokuvat": []}

sali_1 = [x for x in range(1,19)]
                   
sali_2 = [x for x in range(1,41)]

sali_3 = [x for x in range(1,33)]


def tallenna_elokuva(ohjelmalista:dict, elokuva:str, kellonaika:str, sali:int):
    naytos = {
    "elokuva": elokuva,
    "kellonaika": kellonaika,
    "sali": sali,
    "varauslista": []
    }
    ohjelmalista["elokuvat"].append(naytos)
    print(f"Tallennettu elokuva {elokuva}, kellonaikaan {kellonaika}, salissa {sali}")
    with open("elokuvat.json","w") as tiedosto:
        json.dump(ohjelmalista, tiedosto, indent=4)
    
def onko_elokuva(ohjelmalista:dict, elokuva:str):
    with open("elokuvat.json","r") as tiedosto:
        ohjelmalista = json.load(tiedosto)
        if elokuva in ohjelmalista:
            return True
        else:
            return False
      
def poista_elokuva(elokuva:str, kellonaika:str, sali:int):
    # naytos = {
    # "elokuva": elokuva,
    # "kellonaika": kellonaika,
    # "sali": sali,
    # "varauslista": []
    # }

    with open("elokuvat.json","r+") as tiedosto:
        ohjelmalista = json.load(tiedosto)
        i = 0
        while i < len(ohjelmalista["elokuvat"]):
            if elokuva == ohjelmalista["elokuvat"][i]["elokuva"]:
                del ohjelmalista["elokuvat"][i]
            i += 1
        #for i in range(len(ohjelmalista["elokuvat"])):
    #         if elokuva == ohjelmalista["elokuvat"][i]["elokuva"]:
    #             del ohjelmalista["elokuvat"][i]
    with open("elokuvat.json","w") as tiedosto:      
        json.dump(ohjelmalista, tiedosto, indent=4)
          
    

def tulosta_ohjelmalista():
    #if len(ohjelmalista) > 0:
    #   avain = list(ohjelmalista.keys())
     #   arvot = list(ohjelmalista.values())
     #   print("Ohjelmalista: ")
     #   for i in range(len(avain)):
     #       print(f"{avain[i]}, Kello: {arvot[i][0]}, Sali: {arvot[i][1]} ")
    with open("elokuvat.json","r") as tiedosto:
        ohjelmalista = json.load(tiedosto)
        print(ohjelmalista)

def varaus_tietokantaan(elokuva:str, sali:int, paikka:int):
    with open("tietokanta.txt","a") as tk:
        tk.write(f"Varattu liput elokuvaan {elokuva} salissa {sali} istumapaikalta {paikka}" "\n")

def varaukset():
    with open("elokuvat.json","r") as tiedosto:
        ohjelmalista = json.load(tiedosto)
        if valittu in ohjelmalista["elokuvat"]:
            print("Varatut paikat: ",  (valittu["varauslista"]))

def valitut_varaukset():
    valittu["varauslista"].append(paikka)
    with open("elokuvat.json","w") as tiedosto:
        json.dump(ohjelmalista, tiedosto, indent=4)
        

def tulosta_paavalikko(): #Tulostaa järjestelmän päävalikon
    print("Tervetuloa elokuvateatterin varausjärjestelmään.\nValitse käyttötarkoitus.")
    print("1: Ylläpitäjä")
    print("2: Asiakas")
    print("0: Sulje ohjelma")

def tulosta_admin_valikko(): #Tulostaa ylläpitäjän valikon
    print("----------------------------------------")
    print("Elokuvateatterin varausjärjestelmä")
    print("Valitse:")
    print("1: Lisää elokuva ohjelmistoon")
    print("2: Poista elokuva ohjelmistosta")
    print("3: Listaa ohjelmisto")
    print("4: Selaa varauksia")
    print("0: Poistu")
    print("----------------------------------------")

def tulosta_asiakasvalikko(): #Tulostaa asiakkaan valikon
    print("----------------------------------------")
    print("Elokuvateatterin varausjärjestelmä")
    print("Valitse:")
    print("1: Listaa ohjelmisto")
    print("2: Varaa paikka")
    print("0: Poistu")
    print("----------------------------------------")

tulosta_paavalikko()
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
            tulosta_admin_valikko()

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
                    while True:
                        sali = int(input("Salin numero ( 1, 2 tai 3): "))
                        if sali == 1 or sali == 2 or sali == 3:
                            break
                        if sali != 1 or sali != 2 or sali != 3:
                            print("Saleja on vain 1, 2 ja 3. Valitse uudelleen!")
                            
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

                tulosta_admin_valikko()
                
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
        tulosta_asiakasvalikko()
        
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
                
                
                elokuva = input("Valitse elokuva, 0: palaa takaisin: ")
                with open("elokuvat.json","r") as tiedosto:
                    ohjelmalista = json.load(tiedosto)
                    for naytos in ohjelmalista["elokuvat"]:
                        if naytos["elokuva"] == elokuva:
                            valittu = naytos
                            print(valittu)
                                    
        
                    
                        
                    

                while True:
                    try:
                        sali = int(input("Valitse sali: "))
                        if sali == 1 or 2 or 3:
                            break
                        if sali != 1 or 2 or 3:
                            print("Saleja on vain 1, 2 ja 3. Valitse uudelleen!")
                            
                    except ValueError:
                        print("Salin numero pitää olla 1, 2 tai 3.")
 
                if sali == 1:
                    print("___________________")
                    print("|13|14|15|16|17|18|")
                    print("|07|08|09|10|11|12|")
                    print("|01|02|03|04|05|06|")
                    print("|_____Screen______|")
                    varaukset()

                    while True:
                        try:
                            paikka = int(input("Valitse istumapaikka (esim 1, 9, 13): "))
                            if type(paikka) == int:
                                break
                        except ValueError:
                            print("Paikka pitää antaa numerona!")

                    if paikka > len(sali_1) or paikka < 1:
                        print("Paikkaa ei ole! Katso salin istumapaikat ja yritä uudelleen.")
                    elif paikka in valittu["varauslista"]:
                        print("Paikka on jo varattu!")
                    elif len(valittu["varauslista"]) >= 18:
                        print("Sali on täynnä!")
                    else:
                        print("Varattu paikka", paikka)
                        valittu["varauslista"].append(paikka)
                        with open("elokuvat.json","w") as tiedosto:
                            json.dump(ohjelmalista, tiedosto, indent=4)
                        varaus_tietokantaan(elokuva, sali, paikka)
               
                elif sali == 2:
                    print("_______________________________")
                    print("|31|32|33|34|35|36|37|38|39|40|")
                    print("|21|22|23|24|25|26|27|28|29|30|")
                    print("|11|12|13|14|15|16|17|18|19|20|")
                    print("|01|02|03|04|05|06|07|08|09|10|")
                    print("|___________Screen____________|")
                    varaukset()

                    while True:
                        try:
                            paikka = int(input("Valitse istumapaikka (esim 1, 9, 13): "))
                            if type(paikka) == int:
                                break
                        except ValueError:
                            print("Paikka pitää antaa numerona!")

                    if paikka > len(sali_2) or paikka < 1:
                        print("Paikkaa ei ole! Katso salin istumapaikat ja yritä uudelleen.")
                    elif paikka in valittu["varauslista"]:
                        print("Paikka on jo varattu!")
                    elif len(valittu["varauslista"]) >= 40:
                        print("Sali on täynnä!")
                    else:
                        print("Varattu paikka", paikka)
                        valittu["varauslista"].append(paikka)
                        with open("elokuvat.json","w") as tiedosto:
                            json.dump(ohjelmalista, tiedosto, indent=4)
                        varaus_tietokantaan(elokuva, sali, paikka)

                elif sali == 3:
                    print("_________________________")
                    print("|25|26|27|28|29|30|31|32|")
                    print("|17|18|19|20|21|22|23|24|")
                    print("|09|10|11|12|13|14|15|16|")
                    print("|01|02|03|04|05|06|07|08|")
                    print("|________Screen_________|")
                    varaukset()

                    while True:
                        try:
                            paikka = int(input("Valitse istumapaikka (esim 1, 9, 13): "))
                            if type(paikka) == int:
                                break
                        except ValueError:
                            print("Paikka pitää antaa numerona!")

                    if paikka > len(sali_3) or paikka < 1:
                        print("Paikkaa ei ole! Katso salin istumapaikat ja yritä uudelleen.")
                    elif paikka in valittu["varauslista"]:
                        print("Paikka on jo varattu!")
                    elif len(valittu["varauslista"]) >= 32:
                        print("Sali on täynnä!")
                    else:
                        print("Varattu paikka", paikka)
                        valittu["varauslista"].append(paikka)
                        with open("elokuvat.json","w") as tiedosto:
                            json.dump(ohjelmalista, tiedosto, indent=4)
                        varaus_tietokantaan(elokuva, sali, paikka)  
            tulosta_asiakasvalikko()

            while True:
                try:
                    valinta = int(input("Valinta: "))
                    if valinta == 0 or 1 or 2:
                        break
                except ValueError:
                    print("Syöte pitää olla luku, ei kirjain! Vain 1, 2 tai 0!") 

    tulosta_paavalikko()
    while True:
        try:
            valinta = int(input("Valinta: "))
            if valinta == 0 or 1 or 2:
                break
        except ValueError:
            print("Syöte pitää olla luku, ei kirjain! Vain 1, 2 tai 0!")

            

        
