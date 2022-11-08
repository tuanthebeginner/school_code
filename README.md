# csd203code
class Book:
    def __init__(self, code, names, author, price):
        self.code = code
        self.names = names
        self.author = author
        self.price = price

    def info(self):
        print(f'ma so: {self.code}, ten: {self.names}, tac gia: {self.author}, gia: {self.price}')

class BookNode:
    def __init__(self, data, next, prev):
        self.data = data
        self.next = next
        self.prev = prev

    def display(self):
        self.data.info()

class BookDLL:
    def __init__(self):
        self.head = None
        self.tail = None

    def is_empty(self):
        if self.head == None:
            return True
        return False

    def removeHead(self):
        if self.is_empty():
            print('Book DLL is empty')
            return
        if self.head.next == None:
            self.head = None
            self.tail = None
            return

        self.head = self.head.next
        self.head.prev = None

        if self.is_empty():
            self.tail = None

    def addTail(self, newdata):
        new_item = BookNode(newdata, None, None)

        if self.is_empty():
            self.head = new_item
        else:
            self.tail.next = new_item
            self.tail.next.prev = self.tail

        self.tail = new_item

    def addHead(self, newdata):
        new_item = BookNode(newdata, None, None)
        if self.is_empty():
            self.tail = new_item
        else:
            self.head.prev = new_item
            new_item.next = self.head

        self.head = new_item

    def removeTail(self):
        if self.is_empty():
            print('Book DLL is empty')
            return
        if self.head.next == None:
            self.head = None
            self.tail = None
            return

        self.tail = self.tail.prev
        self.tail.next = None

        if self.is_empty():
            self.head = None

    def traversal(self):
        if self.is_empty():
            print("Book DLL is empty")
            return
        current = self.head
        while current != None:
            current.display()
            current = current.next

    def isDuplicated(self, _id):
        if self.is_empty():
            return False
        current = self.head
        while current != None:
            if (current.data.id == _id):
                return True
            current = current.next
        return False

    def update(self, newData):
        if self.is_empty():
            print("Book DLL is empty")
            return
        current = self.head
        while current != None:
            if (current.data.id == newData.id):
                current.data.names = newData.names
                current.data.address = newData.address
                current.data.score = newData.score
                return
            current = current.next


menu_options = {
    1: 'Thêm sinh viên (CREATE)',
    2: 'Hiển thị danh sách (READ)',
    3: 'Hiển thị thông tin sinh viên (READ)',
    4: 'Cập nhật sinh viên (UPDATE)',
    5: 'Xóa sinh viên khi biết mã số (DELETE)',
    6: 'Remove head',
    7: 'Remove tail',
    'Others': 'Thoát chương trình CRUD'
}


def print_menu():
    for key in menu_options.keys():
        print(key, '--', menu_options[key])


stuList = BookDLL()

while (True):
    print_menu()
    userChoice = ''
    try:
        userChoice = int(input('Nhap tuy chon: '))
    except:
        print('Nhap sai, moi nhap lai....')
        continue

    if userChoice == 1:
        maso = input("Nhap ma so: ")
        ten = input("Nhap ten: ")
        tacgia = input("Nhap tac gia: ")
        gia = float(input("Nhap gia ca: "))
        sach = Book(maso, ten, tacgia, gia)
        if (stuList.isDuplicated(maso) == False):
            stuList.addTail(sach)
    elif userChoice == 5:
        stuList.traversal()
    elif userChoice == 3:
        maso = input("Nhap ma so sach can cap nhat: ")
        ten = input("Cap nhat ten: ")
        tacgia = input("Cap nhat tac gia: ")
        gia = float(input("Cap nhat gia: "))
        sach = Book(maso, ten, tacgia, gia)
        stuList.update(sach)
    else:
        print('bye')
        break
