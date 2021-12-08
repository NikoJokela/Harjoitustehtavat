
ohjelmalista = {}
sali_1 = [x for x in range(1,19)]
varaus_1 = []
sali_2 = [x for x in range(1,41)]
varaus_2 = []
sali_3 = [x for x in range(1,33)]
varaus_3 = []

def tallenna_elokuva(ohjelmalista:dict, elokuva:str, kellonaika:str, sali:int):
    ohjelmalista[elokuva] = (kellonaika, sali)
    esitys = (elokuva, kellonaika, sali) #turhaa
    return esitys #turhaa
    
    
def onko_elokuva(ohjelmalista:dict, elokuva:str) -> bool:
    if elokuva in ohjelmalista:
        return True
    else:
        return False

def onko_elokuva_kellonaika(ohjelmalista:dict, elokuva:str, kellonaika:str) -> bool: #tarkastaa onko tietty elokuva tiettyyn aikaan ohjelmistossa
    if (elokuva and kellonaika) in ohjelmalista:
        return True
    else:
        return False       
        
def poista_elokuva(ohjelmalista:dict, elokuva:str, kellonaika:str) -> bool: 
    del ohjelmalista[elokuva]
    return True
    

def salin_elokuvat(ohjelmalista:dict, sali:int) -> list: #Listataan halutun salin elokuvat
    elokuvalista = []
    arvot = list(ohjelmalista.values())
    for i in arvot:
        if sali in i:
            elokuvalista.append(i)
    return elokuvalista


print("Tervetuloa elokuvateatterin varausjärjestelmään.\nValitse käyttötarkoitus.")
print("1: Ylläpitäjä")
print("2: Asiakas")
print("0: Sulje ohjelma")
valinta = int(input("Valinta: "))
while valinta != 0:
    if valinta == 1:
        print("----------------------------------------")
        print("Elokuvateatterin varausjärjestelmä")
        print("Valitse:")
        print("1: Lisää elokuva ohjelmistoon")
        print("2: Poista elokuva ohjelmistosta")
        print("3: Listaa ohjelmisto")
        print("4: Selaa varauksia")
        print("0: Poistu")
        print("----------------------------------------")
        valinta = int(input("Valinta: "))

        while valinta != 0:     #Ylläpitäjän käyttöliittymä

            if valinta == 1:
                elokuva = input("Elokuvan nimi: ")
                kellonaika = input("Lisää kellonaika: ")
                sali = input("Salin numero: ")
                tallenna_elokuva(ohjelmalista, elokuva, kellonaika, sali)
            
            elif valinta == 2:
                elokuva = input("Anna elokuvan nimi: ")
                kellonaika = input("Anna kellonaika: ")
                poista_elokuva(ohjelmalista, elokuva, kellonaika)
                print(f"Elokuva {elokuva} kello {kellonaika} poistettu")
            
            elif valinta == 3:

                avain = list(ohjelmalista.keys())
                arvot = list(ohjelmalista.values())
                print("Ohjelmalista: ")
                for i in range(len(avain)):
                    print(f"{avain[i]}, Kello: {arvot[i][0]}, Sali: {arvot[i][1]} ")
            
            elif valinta == 4:
                pass
                
                

            print("----------------------------------------")
            print("Elokuvateatterin varausjärjestelmä")
            print("Valitse:")
            print("1: Lisää elokuva ohjelmistoon")
            print("2: Poista elokuva ohjelmistosta")
            print("3: Listaa ohjelmisto")
            print("4: Selaa varauksia")
            print("0: Poistu")
            print("----------------------------------------")
            valinta = int(input("Valinta: "))   # KORJAA ETTEI CRASHAA JOS VÄÄRÄ INPUT 

    elif valinta == 2:
        print("----------------------------------------")
        print("Elokuvateatterin varausjärjestelmä")
        print("Valitse:")
        print("1: Listaa ohjelmisto")
        print("2: Varaa paikka")
        print("0: Poistu")
        print("----------------------------------------")
        valinta = int(input("Valinta: "))

        while valinta != 0: #Asiakkaan käyttöliittymä
            if valinta == 1:
                if len(ohjelmalista) > 0:
                    avain = list(ohjelmalista.keys())
                    arvot = list(ohjelmalista.values())
                    print("Ohjelmalista: ")
                    for i in range(len(avain)):
                        print(f"{avain[i]}, Kello: {arvot[i][0]}, Sali: {arvot[i][1]} ")
                
                
            elif valinta == 2:
                
                while True:
                    elokuva = input("Valitse elokuva, 0: palaa takaisin: ")
                    if onko_elokuva(ohjelmalista, elokuva):
                        break
                    if elokuva == "0":
                        break
                    if not onko_elokuva(ohjelmalista, elokuva):
                        print("Elokuvaa ei ole ohjelmistossa!")
                    

                    
                
                sali = int(input("Valitse sali: "))
                        
                if sali == 1:
                    print("___________________")
                    print("|13|14|15|16|17|18|")
                    print("|07|08|09|10|11|12|")
                    print("|01|02|03|04|05|06|")
                    print("|_____Screen______|")
                    print("Varatut paikat: ", varaus_1)

                    paikka = int(input("Valitse istumapaikka (esim 1, 9, 13): "))
                    if paikka > len(sali_1) or paikka < 1:
                        print("Paikkaa ei ole! Katso salin istumapaikat ja yritä uudelleen.")
                    if paikka in varaus_1:
                        print("Paikka on jo varattu!")
                    if len(varaus_1) >= 18:
                        print("Sali on täynnä!")
                    if paikka in sali_1 and paikka not in varaus_1 and len(varaus_1) < 18:
                        print("Varattu paikka", paikka)
                        varaus_1.append(paikka)
                    
                elif sali == 2:
                    print("_______________________________")
                    print("|31|32|33|34|35|36|37|38|39|40|")
                    print("|21|22|23|24|25|26|27|28|29|30|")
                    print("|11|12|13|14|15|16|17|18|19|20|")
                    print("|01|02|03|04|05|06|07|08|09|10|")
                    print("|___________Screen____________|")
                    print("Varatut paikat: ", varaus_2)

                    paikka = int(input("Valitse istumapaikka (esim 1, 9, 13): "))
                    if paikka > len(sali_2) or paikka < 1:
                        print("Paikkaa ei ole! Katso salin istumapaikat ja yritä uudelleen.")
                    if paikka in varaus_2:
                        print("Paikka on jo varattu!")
                    if len(varaus_2) >= 40:
                        print("Sali on täynnä!")
                    if paikka in sali_2 and paikka not in varaus_2 and len(varaus_2) < 40:
                        print("Varattu paikka", paikka)
                        varaus_2.append(paikka)

                elif sali == 3:
                    print("_________________________")
                    print("|25|26|27|28|29|30|31|32|")
                    print("|17|18|19|20|21|22|23|24|")
                    print("|09|10|11|12|13|14|15|16|")
                    print("|01|02|03|04|05|06|07|08|")
                    print("|________Screen_________|")
                    print("Varatut paikat: ", varaus_2)

                    paikka = int(input("Valitse istumapaikka (esim 1, 9, 13): "))
                    if paikka > len(sali_3) or paikka < 1:
                        print("Paikkaa ei ole! Katso salin istumapaikat ja yritä uudelleen.")
                    if paikka in varaus_3:
                        print("Paikka on jo varattu!")
                    if len(varaus_3) >= 32:
                        print("Sali on täynnä!")
                    if paikka in sali_3 and paikka not in varaus_3 and len(varaus_3) < 32:
                        print("Varattu paikka", paikka)
                        varaus_3.append(paikka)
                
            print("----------------------------------------")
            print("Elokuvateatterin varausjärjestelmä")
            print("Valitse:")
            print("1: Listaa ohjelmisto")
            print("2: Varaa paikka")
            print("0: Poistu")
            print("----------------------------------------")
            valinta = int(input("Valinta: "))    

    print("Tervetuloa elokuvateatterin varausjärjestelmään.\nValitse käyttötarkoitus.")
    print("1: Ylläpitäjä")
    print("2: Asiakas")
    print("0: Sulje ohjelma")
    valinta = int(input("Valinta: "))

            

        


        

        
