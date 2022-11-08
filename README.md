# csd203code
class Pet:

    # Pet: id, nickName, age, weight. 
    # your code here.
    def __init__(self, id, nickName, age, weight):
        self.id = id
        self.nickName = nickName
        self.age = age
        self.weight = weight
    def print(self):
        print(self.id, self.nickName, self.age, self.weight)
        
class Node:

    def __init__(self,data):
        self.data = data
        self.next = None
        self.prev = None


class DoubleLinkedList:

    def __init__(self):
        self.head = None
        
    # function: add new PUPPY into List
    def add(self, newPuppy):
        # your code here
        if self.head == None:
            self.head = newPuppy
        else:
            tmp = self.head
            while tmp.next is not None:
                tmp = tmp.next
            tmp.next = newPuppy
            newPuppy.prev = tmp
            
    # function: search PUPPY based name
    def search(self, searchName):
        # your code here:
        tmp = self.head
        while tmp is not None:
            if searchName in tmp.data.nickName:
                tmp.data.print()
            tmp = tmp.next
            
    # function: remove puppy based id
    def remove(self, id):
        # your code here
        if self.head.data.id == id:
            self.head = self.head.next
        else:
            prev = None
            tmp = self.head
            while tmp is not None:
                if tmp.data.id == id:
                    if tmp.next is None:
                        prev.next = None
                        tmp.next = None
                    else:
                        prev.next = tmp.next
                        tmp.next.prev = prev
                prev = tmp
                tmp = tmp.next
                
                
    # function: display puppy list
    def display(self):
        # your code here
        tmp = self.head
        while tmp is not None:
            tmp.data.print()
            tmp = tmp.next
    def check_exist(self,id):
        tmp = self.head
        while tmp is not None:
            if tmp.data.id == id:
                return True
            tmp = tmp.next
        return False



def print_menu():

    print("1. Add puppy.")
    print("2. Search puppy by name.")
    print("3. Display all puppy.")
    print("4. Remove puppy by ID.")
    print("5. Exist the menu.")



print_menu()

l = DoubleLinkedList()

user_choice = int(input("Enter your choice:"))
while user_choice in [1,2,3,4]:

    if user_choice == 1:
        id = input("Enter puppy id:")
        if l.check_exist(id) == True:
            print("Puppy existed.")
        else:
            name = input("Enter puppy nickname:")
            age = int(input("Enter puppy age:"))
            weight = float(input("Enter puppy weight:"))
            pet = Pet(id, name, age, weight)
            data = Node(pet)
            l.add(data)
    elif user_choice ==2:
        name = input("Enter words in name of puppy:")
        l.search(name)
    elif user_choice == 3:
        l.display()
    elif user_choice == 4:
        id = input("Enter puppy id to delete:")
        if l.check_exist(id) == False:
            print("Pet not exist.")
        else:
            l.remove(id)
    print_menu()
    user_choice = int(input("Enter your choice:"))
