while True:
    c = input("write something: ")
    if c == "stop":
        break
    if len(c) < 2:
        print("write more")
        continue
    if len(c) > 2:
        print(len(c))
        continue
print("the program is finished")

