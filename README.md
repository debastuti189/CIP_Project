# CIP_Project
CIP_FinalWeek
import json
from simpleimage import SimpleImage

RED_IN_IRON=220
RED_IN_ZINC=53
RED_IN_BAUXITE=82

def make_a_file():
    data={"Iron Ore":{"Origin":"Sedimentation","Mode of Occurence":["Magmatic Deposit",
    "Bedded Deposit","Residual Concentration Deposit"],"Tonnage":220},
    "Zinc":{"Origin":"Contact Metasomatism","Mode of Occurence":["Veins","Disseminations","Cavity Fillings"],"Tonnage":4},
    "Bauxite":{"Origin":"Chemical sedimentation","Mode of Occurence":["Blanket Deposit","Interstratified Deposit","Pocket Deposit"],"Tonnage":26}}

    with open("data.json","w")as f:
        json.dump(data, f, indent=4)

def mineral_info():
    with open("data.json") as f:
     info=json.load(f)
     wish="Y"
     while wish=="Y":
        choice= input("Enter your choice: Iron Ore/Bauxite/Zinc ")
        if (choice=='Iron Ore'):
            print(choice+":")
            print(info["Iron Ore"])
        elif(choice=='Bauxite'):
            print(choice+":")
            print(info["Bauxite"])
        elif(choice=='Zinc'):
            print(choice+":")
            print(info["Zinc"])
        else:
            print("You have entered an invalid choice--Please enter a valid choice")
        get_map(choice)
        wish=input("Do you wish to continue: Y/N ")

def get_map(choice):
    image1=SimpleImage('Blank_Map.JPG')
    image2=SimpleImage('Mineral_Map.JPG')
    wid=image1.width
    ht=image1.height
    new=SimpleImage.blank(wid,ht)
    if(choice=="Bauxite"):
     for p2 in image2:
       x=p2.x
       y=p2.y
       if p2.red==RED_IN_BAUXITE:
           image1.set_pixel(x,y,image2.get_pixel(x,y))
     image1.show()
    if(choice=="Iron Ore"):
     for p2 in image2:
       x=p2.x
       y=p2.y
       if p2.red==RED_IN_IRON:
           image1.set_pixel(x,y,image2.get_pixel(x,y))
     image1.show()
    if(choice=="Zinc"):
     for p2 in image2:
       x=p2.x
       y=p2.y
       if p2.red==RED_IN_ZINC:
           image1.set_pixel(x,y,image2.get_pixel(x,y))
     image1.show()

def get_info():
    information=[]
    name_old=[]
    name_new=[]
    with open("data.json") as f:
        info=json.load(f)
        information.append(info["Iron Ore"]["Tonnage"])
        information.append(info["Zinc"]["Tonnage"])
        information.append(info["Bauxite"]["Tonnage"])

        print("Quantity of mineral ore produced as found on file in million tonnes in 2020")
        for i in range(len(information)):
            if (information[i]==info["Iron Ore"]["Tonnage"]):
                name_old.append("Iron Ore")
            elif (information[i]==info["Bauxite"]["Tonnage"]):
                name_old.append("Bauxite")
            elif(information[i]==info["Zinc"]["Tonnage"]):
                name_old.append("Zinc")
        for j in range(len(information)):
            print(name_old[j]+" "+str(information[j]))

        print("Quantity of mineral ore produced from minimum to maximum in million tonnes in 2020")

        information.sort()
        for i in range(len(information)):
            if (information[i]==info["Iron Ore"]["Tonnage"]):
                name_new.append("Iron Ore")
            elif (information[i]==info["Bauxite"]["Tonnage"]):
                name_new.append("Bauxite")
            elif(information[i]==info["Zinc"]["Tonnage"]):
                name_new.append("Zinc")
        for j in range(len(information)):
            print(name_new[j]+" "+str(information[j]))
        
        print("The minimum production was of the mineral"+" "+name_new[0])
        print("The minimum production was of the mineral"+" "+name_new[len(name_new)-1])


def main():
    make_a_file()
    mineral_info()
    get_info()

    
if __name__ == '__main__':
    main()
