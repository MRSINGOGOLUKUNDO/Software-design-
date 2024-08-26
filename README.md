# Software-design-
class Student:

    def __init__(self, id, name, age, major):

        self.id = id

        self.name = name

        self.age = age

        self.major = major 



    def update(self, name=None, age=None, major=None):

        if name is not None:

            self.name = name

        if age is not None:

            self.age = age

        if major is not None:

            self.major = major 



    def __str__(self):

        return f"ID: {self.id}, Name: {self.name}, Age: {self.age}, Major: {self.major}"





class StudentDatabase:

    def __init__(self):

        self.students = {} 



    def add_student(self, student):

        self.students[student.id] = student 



    def remove_student(self, student_id):

        if student_id in self.students:

            del self.students[student_id] 



    def get_student(self, student_id):

        return self.students.get(student_id) 



    def get_all_students(self):

        return list(self.students.values())





class StudentManagementSystem:

    def __init__(self):

        self.database = StudentDatabase() 



    def add_student(self):

        id = int(input("Enter student ID: "))

        name = input("Enter student name: ")

        age = int(input("Enter student age: "))

        major = input("Enter student major: ")

        student = Student(id, name, age, major)

        self.database.add_student(student) 



    def delete_student(self):

        id = int(input("Enter student ID to delete: "))

        self.database.remove_student(id) 



    def update_student(self):

        id = int(input("Enter student ID to update: "))

        student = self.database.get_student(id)

        if student:

            name = input("Enter new name (leave blank to keep current): ") or None

            age_str = input("Enter new age (leave blank to keep current): ")

            age = int(age_str) if age_str else None

            major = input("Enter new major (leave blank to keep current): ") or None

            student.update(name=name, age=age, major=major)

        else:

            print("Student not found.") 



    def show_all_students(self):

        students = self.database.get_all_students()

        if students:

            for student in students:

                print(student)

        else:

            print("No students found.") 



    def menu(self):

        while True:

            print("\nStudent Management System Menu:")

            print("1. Add Student")

            print("2. Delete Student")

            print("3. Update Student Information")

            print("4. Show All Students")

            print("5. Exit") 



            choice = input("Enter your choice (1-5): ")

            if choice == "1":

                self.add_student()

            elif choice == "2":

                self.delete_student()

            elif choice == "3":

                self.update_student()

            elif choice == "4":

                self.show_all_students()

            elif choice == "5":

                break

            else:

                print("Invalid choice. Please try again.")





# Example usage

if __name__ == "__main__":

    system = StudentManagementSystem()

    system.menu()

