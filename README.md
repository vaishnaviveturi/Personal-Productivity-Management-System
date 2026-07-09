
# Personal Productivity Management System

tasks=[]
students=[]
expenses=[]

def get_int(msg):
    while True:
        try:
            return int(input(msg))
        except ValueError:
            print("Enter a valid number.")

def get_float(msg):
    while True:
        try:
            return float(input(msg))
        except ValueError:
            print("Enter a valid amount/marks.")

def todo_menu():
    while True:
        print("\n--- TO DO LIST ---")
        print("1.Add Task\n2.View Tasks\n3.Update Task\n4.Delete Task\n5.Search Task\n6.Mark Completed\n7.View Completed\n8.View Pending\n9.Back")
        c=input("Enter choice: ")
        if c=="1":
            tasks.append({"task":input("Enter task: "),"status":"Pending"})
        elif c=="2":
            if not tasks: print("No tasks available.")
            else:
                for i,t in enumerate(tasks,1):
                    print(f"{i}. {t['task']} - {t['status']}")
        elif c=="3":
            if not tasks: print("No tasks."); continue
            n=get_int("Task number: ")
            if 1<=n<=len(tasks):
                tasks[n-1]["task"]=input("New task: ")
            else: print("Invalid task number.")
        elif c=="4":
            if not tasks: print("No tasks."); continue
            n=get_int("Task number: ")
            if 1<=n<=len(tasks):
                print("Deleted:",tasks.pop(n-1)["task"])
            else: print("Invalid task number.")
        elif c=="5":
            s=input("Search: ").lower(); f=False
            for t in tasks:
                if s in t["task"].lower():
                    print(t["task"],"-",t["status"]); f=True
            if not f: print("Task not found.")
        elif c=="6":
            if not tasks: print("No tasks."); continue
            n=get_int("Task number: ")
            if 1<=n<=len(tasks):
                tasks[n-1]["status"]="Completed"
            else: print("Invalid task number.")
        elif c=="7":
            f=[t for t in tasks if t["status"]=="Completed"]
            if not f: print("No completed tasks.")
            else:
                for t in f: print(t["task"])
        elif c=="8":
            f=[t for t in tasks if t["status"]=="Pending"]
            if not f: print("No pending tasks.")
            else:
                for t in f: print(t["task"])
        elif c=="9": break
        else: print("Invalid choice.")

def student_menu():
    while True:
        print("\n--- STUDENT MANAGEMENT ---")
        print("1.Add\n2.View\n3.Search\n4.Update\n5.Delete\n6.Topper\n7.Average\n8.Back")
        c=input("Enter choice: ")
        if c=="1":
            students.append({"name":input("Name: "),"roll":input("Roll: "),"marks":get_float("Marks: ")})
        elif c=="2":
            if not students: print("No students.")
            else:
                for s in students: print(s)
        elif c=="3":
            r=input("Roll: "); f=False
            for s in students:
                if s["roll"]==r: print(s); f=True
            if not f: print("Student not found.")
        elif c=="4":
            r=input("Roll: "); f=False
            for s in students:
                if s["roll"]==r:
                    s["name"]=input("New Name: "); s["marks"]=get_float("New Marks: "); f=True
            if not f: print("Student not found.")
        elif c=="5":
            r=input("Roll: "); f=False
            for s in students:
                if s["roll"]==r:
                    students.remove(s); f=True; break
            if not f: print("Student not found.")
        elif c=="6":
            if students: print("Topper:",max(students,key=lambda x:x["marks"]))
            else: print("No students.")
        elif c=="7":
            if students: print("Average:",sum(s["marks"] for s in students)/len(students))
            else: print("No students.")
        elif c=="8": break
        else: print("Invalid choice.")

def expense_menu():
    while True:
        print("\n--- EXPENSE TRACKER ---")
        print("1.Add\n2.View\n3.Search\n4.Update\n5.Delete\n6.Total\n7.Highest\n8.Back")
        c=input("Enter choice: ")
        if c=="1":
            expenses.append({"item":input("Item: "),"amount":get_float("Amount: ")})
        elif c=="2":
            if not expenses: print("No expenses.")
            else:
                for e in expenses: print(e)
        elif c=="3":
            q=input("Search: ").lower(); f=False
            for e in expenses:
                if q in e["item"].lower(): print(e); f=True
            if not f: print("Expense not found.")
        elif c=="4":
            it=input("Item: "); f=False
            for e in expenses:
                if e["item"]==it:
                    e["item"]=input("New Item: "); e["amount"]=get_float("New Amount: "); f=True
            if not f: print("Expense not found.")
        elif c=="5":
            it=input("Item: "); f=False
            for e in expenses:
                if e["item"]==it:
                    expenses.remove(e); f=True; break
            if not f: print("Expense not found.")
        elif c=="6":
            print("Total Expense =",sum(e["amount"] for e in expenses))
        elif c=="7":
            if expenses: print("Highest Expense:",max(expenses,key=lambda x:x["amount"]))
            else: print("No expenses.")
        elif c=="8": break
        else: print("Invalid choice.")

while True:
    print("\n===== PERSONAL PRODUCTIVITY MANAGEMENT SYSTEM =====")
    print("1.To-Do List\n2.Student Management\n3.Expense Tracker\n4.Exit")
    ch=input("Enter choice: ")
    if ch=="1": todo_menu()
    elif ch=="2": student_menu()
    elif ch=="3": expense_menu()
    elif ch=="4":
        print("Thank You!")
        break
    else:
        print("Invalid Choice! Please try again.")
