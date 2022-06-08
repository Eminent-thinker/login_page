# login_page
import tkinter.messagebox
from tkinter import * 
from PIL import Image, ImageTk
from random import choice, randint, shuffle

    
def password_generator():
       letters = ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z", "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"]
       characters = ["@", "#", "&","(", ")","/", "!", "?", "£", "$", "¥", "{", "}"]
       numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0"]
       list_of_letters = [choice(letters) for x in range(randint(4,8))]
       list_of_characters = [choice(characters) for x in range(randint(2,4))]
       list_of_numbers = [choice(numbers) for x in range(randint(2,4))]
       list_of_password = list_of_letters + list_of_characters + list_of_numbers
       shuffle(list_of_password)
       password = ''.join(list_of_password)
       password_entry.insert(0,password)
def add():
       website = website_entry.get()
       username = username_entry.get()
       password = password_entry.get()
       if website == '' and password:
          web = tkinter.messagebox.showwarning("showwarning", "please, provide the website name!")
          print(web)
       elif password == '' and website:
          pas = tkinter.messagebox.showwarning("showwarning", "please, provide the password!")
          print(pas)
       elif password == '' and website == '' :
          web_pass = tkinter.messagebox.showwarning("showwarning", "please, provide the website name and the password!")
          print(web_pass)
       else:
          isYes = tkinter.messagebox.askyesno("Preview", f"website: {website}\nusername: {username}\npassword: {password}\nAre you sure you want to continue?")
          print(isYes)
          if isYes:
             filename = "data.txt"
             with open(filename, 'a') as file:
                file.write(f"{website} | {username} | {password}\n\n")
root = Tk()
canvas = Canvas(width = 400, height = 400, bg = "white")
canvas.grid(row= 0, column = 0, columnspan = 3)
photo = ImageTk.PhotoImage(Image.open("padlock.jpg"))
canvas.create_image(10,-10, anchor = NW, image = photo)
website_label = Label(text = "Website:")
website_entry =Entry()
website_entry.grid(row =1, column= 1, ipadx = 180, ipady = 9, columnspan = 4)
username_entry = Entry()
username_entry.insert(0, "Eminent-thinker")
username_entry.grid(row = 2, column = 1, ipadx = 180, ipady = 9, columnspan = 3)
password_entry = Entry()
password_entry.grid(row = 3, column = 1, ipady = 13)
username_label = Label(text = "Username:")
password_label = Label(text = "Password: ")
generator_button = Button(text = 'Generate password', command = password_generator)
add_button = Button(text = 'add', command = add)
website_label.grid(row = 1, column = 0)
username_label.grid(row = 2, column = 0)
password_label.grid(row= 3, column = 0)
generator_button.grid(row =3, column =2)
add_button.grid(row = 4, column = 0, ipadx =393, columnspan = 3)
mainloop()
