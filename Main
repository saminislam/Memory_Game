## TO BE USED WITH PYTHON

from tkinter import *
from tkinter import ttk
from tkinter.ttk import *
from functools import partial
import tkinter as tk
import random
import time



#### GAME FUNCTIONS ####

def shuffle_deck(deck):
    '''(list of str)->None
       Shuffles the given list of strings representing the playing deck    
    '''
    random.shuffle(deck)

   

def create_board(size):
    '''int->list of str
       Precondition: size is even positive integer between 2 and 52
       Returns a rigorous deck (i.e. board) of a given size.
    '''
    board = [None]*size 

    letter='A'
    for i in range(len(board)//2):
          board[i]=letter
          board[i+len(board)//2 ]=board[i]
          letter=chr(ord(letter)+1)
    return board


def read_raw_board(file):
    '''str->list of str
    Returns a list of strings represeniting a deck of cards that was stored in a file. 
    The deck may not necessarifly be playable
    '''
    raw_board = open(file).read().splitlines()
    for i in range(len(raw_board)):
        raw_board[i]=raw_board[i].strip()
    return raw_board


def clean_up_board(l):
    '''list of str->list of str

    The functions takes as input a list of strings representing a deck of cards. 
    It returns a new list containing the same cards as l except that
    one of each cards that appears odd number of times in l is removed
    and all the cards with a * on their face sides are removed
    '''
    print("\nRemoving one of each cards that appears odd number of times and removing all stars ...\n")
    l.sort()
    length=len(l)
    i=0
    playable_board=[]
    counter=0
    while ( i<length):
        counter = l.count(l[i])
        if counter%2 == 0:
            if l[i] == '*':
                pass
            else:
                playable_board.append(l[i])
        if counter%2==1:
            if l[i]=='*':
                pass
        if counter/2>1:
            if l[i] =='*':
                i=i+1
                pass
            else:
                
                counter=counter-1
                for y in range(counter):
                    playable_board.append(l[i])
                i=i+counter+1
        else:
            i=i+1
    return playable_board






def countdown(count):
    # change text in label
    if lbl3.winfo_exists():
        lbl3['text'] = "You have " + str(count) + " seconds to memorize the following"

    if count > 0:
        # call countdown again after 1000ms (1s)
        if lbl3.winfo_exists():
            window.after(1000, countdown, count-1)
    if count == 0:
        for x in range(size):
            global button_output
            button_output = (button_id[x])
            button_output.configure(text = "*")
            button_output.configure(state = "normal")
        lbl3['text'] = "Good Luck :)"

    return


def attempt_inc():
    global trial_num
    lbl4['text'] = "Attempt Number:" + str(trial_num)
    return 
    



def gametime(counter):
    global trial_num
    global PrevButtonID
    counter_of_disable = 0
    global bname
    bname = button_id[counter]
    bname.configure(text = created_board[counter])
    dull_side[counter] = created_board[counter]
    ButtonID = counter
    bname.configure(state = "disabled")
    for x in range(size):
        if (button_id[x]['state'] == "disabled"):
            counter_of_disable = counter_of_disable + 1
    if (counter_of_disable%2!=0):
        PrevButtonID = counter
    if (counter_of_disable%2 ==0):
        if(created_board[PrevButtonID] == created_board[counter]):
            bname.configure(text = created_board[counter])

            trial_num = trial_num + 1
            
            attempt_inc()    

            
            dull_side[counter] = created_board[counter]
        elif(created_board[PrevButtonID] != created_board[counter]):
            dull_side[PrevButtonID] = '*'
            dull_side[counter] = '*'
            
            for x in range(size):
                button_id[x]['state'] = "disabled"
                window.update()
            window.after(1000)
            for x in range(size):
                if dull_side[x] == '*':
                    button_id[x]['state'] = "normal"
                    
            bname.configure(text = '*')
            bname.configure(state = "normal")
            bname = button_id[PrevButtonID]
            bname.configure(text = '*')
            bname.configure(state = "normal")

            trial_num = trial_num + 1
            
            attempt_inc()
    if '*' not in dull_side:
        lbl3['text'] = "Congratulations! You have completed the Memory game"

    
    return
            
            
    







def game_begin(picked_dif, dev_mode):
    global lbl3
    if (picked_dif == 6):
        window.title("Easy Difficulty")
    elif (picked_dif == 10):
        window.title("Medium Difficulty")
    elif (picked_dif == 12):
        window.title("Hard Difficulty")
    elif (picked_dif == 16):
        window.title("Brainiac Difficulty")
    else:
        window.title("Developer Mode")

    if (dev_mode == False):
        global created_board
        created_board = create_board(picked_dif)
        shuffle_deck(created_board)
        global size
        size = len(created_board)
        global dull_side
        dull_side = ['*']*size
    

    if (dev_mode == True):
        
        created_board = board_dev
        shuffle_deck(created_board)
        size = picked_dif_dev
        dull_side = ['*']*size
        

    
    counter = 0
    global total_counter
    total_counter = 0
    row_ = 1
    counter = 0
    timer = 10
    
    lbl3 = tk.Label(window, bg = "#89cff0")
    lbl3.grid(columnspan= 5)
    countdown(10)

    global button_id
    button_id = []    
    
    
    
    
    for item in created_board:
        if (counter//4 ==0):
            global b
            b = tk.Button(window,font = ('arial',20,'bold'),width=10, text = item,state = "disabled", command = partial(gametime,total_counter))
            button_id.append(b)
            b.grid(row = row_,column = counter,sticky = W)
            counter = counter + 1
            total_counter = total_counter + 1
        else:
            row_ = row_+ 1
            counter = 0
            b = tk.Button(window,font = ('arial',20,'bold'),width=10, text = item,state = "disabled", command = partial(gametime,total_counter))
            button_id.append(b)
            b.grid(row = row_, column = counter,sticky = W)
            counter = counter + 1
            total_counter = total_counter + 1


    global lbl4, lbl5
    lbl4 = tk.Label(window,bg = "#89cff0")
    lbl4.grid(row = row_ + 2, columnspan = 2, sticky = W,pady = 5)
    lbl4['text'] = "Attempt Number: 0"
    lbl5 = tk.Label(window, bg = "#89cff0")
    lbl5.grid(row = row_ + 1, columnspan = 2, sticky = W, pady = 5)
    lbl5['text'] = "Best Number of Guesses:" + str(size//2)

    global exit_button, main_menu_button
    exit_button = tk.Button(window, text = "Exit Application", command = window.destroy)
    exit_button.grid(row = row_ + 5, column = 5 ,columnspan = 2, sticky = E, pady = 10)
    main_menu_button = tk.Button(window, text = "Exit To Main Menu", command = clear_menu)
    main_menu_button.grid(row = row_ + 6, column = 5, columnspan = 2, sticky = E, pady = 10)    
                            
    return

    

def clear_menu():
    lbl3.destroy()
    lbl4.destroy()
    lbl5.destroy()
    
    for x in range(size):
        bname = button_id[x]
        bname.destroy()
    exit_button.destroy()
    main_menu_button.destroy()
    main_menu()
        

#### GUI FUNCTIONS ####
# GUI CONSTANTS



def clicked():
    
    lbl1.destroy()
    rad1.destroy()
    rad2.destroy()
    rad3.destroy()
    btn1.destroy()
    global picked
    picked = selected.get()
    difficulty_selection(picked)

def clicked1():
    global picked_dif
    picked_dif = selected_dif.get()
    rad4.destroy()
    rad5.destroy()
    rad6.destroy()
    rad7.destroy()
    lbl2.destroy()
    btn2.destroy()
    #DEV MODE FLAG
    global dev_mode
    dev_mode = False
    game_begin(picked_dif, dev_mode)


def read_raw_file():
    file_name = e1.get()
    file_name = file_name.strip()
    global board_dev, picked_dif_dev
    board_dev = read_raw_board(file_name)
    board_dev = clean_up_board(board_dev)
    picked_dif_dev = len(board_dev)
    lbl6.destroy()
    e1.destroy()
    lbl7.destroy()
    lbl8.destroy()
    btn10.destroy()
    global dev_mode
    dev_mode = True
    game_begin(picked_dif_dev,dev_mode)
    
    

def difficulty_selection(picked):
    if (picked == 1):
        global rad4, rad5, rad6, rad7, lbl2, btn2
        mycolour = "#89cff0"
        
        rad4 = tk.Radiobutton(window, text = 'Easy', value = 6, variable = selected_dif, background = mycolour)
        rad5 = tk.Radiobutton(window, text = 'Medium', value = 10, variable = selected_dif, background = mycolour)
        rad6 = tk.Radiobutton(window, text = 'Hard', value = 12, variable = selected_dif, background = mycolour)
        rad7 = tk.Radiobutton(window, text = 'Brainiac', value = 16, variable = selected_dif, background = mycolour)

        rad4.grid(column = 1, row = 5, padx = 150, pady = 2, sticky = W)
        rad5.grid(column = 1, row = 6, padx = 150, pady = 2, sticky = W)
        rad6.grid(column = 1, row = 7, padx = 150, pady = 2, sticky = W)
        rad7.grid(column = 1, row = 8, padx = 150, pady = 2, sticky = W)

        lbl2 = tk.Label(window, text = "Pick Difficulty", bg = mycolour, borderwidth = 3, relief = "raised")
        lbl2.configure(font = ("arial",20))
        lbl2.grid(column = 1, row = 1, padx = 150, pady = 10, sticky = W)

        global picked_dif 
        picked_dif = selected_dif.get()

        btn2 = Button(window, text = 'Enter', command = clicked1)
        btn2.grid(column = 1, row = 9, padx = 150, sticky = W)


    if (picked == 2):
        global lbl6 , e1 ,btn10, lbl7, lbl8 
        lbl6 = tk.Label(window, text = "Input File Name", background = "#89cff0", font = ("arial",16) )
        lbl6.grid(row = 1, column = 0, padx = 10, pady = 5, sticky = W)
        e1 = tk.Entry(window,  width = 45, font = ("arial",18))
        e1.grid(row = 2, column = 0, sticky = W)
        btn10 = tk.Button(window, text = "Enter", font = 20, width = 10, height = 2,command = read_raw_file)
        btn10.grid(row =2, column = 1, sticky = W)
        lbl7 = tk.Label(window, text = "ATTENTION: All odd characters in file will be made even and all '*' will be removed.",background = "#89cff0")
        lbl7.grid(row = 3, column = 0, columnspan = 8, sticky = W)
        lbl8 = tk.Label(window, text = "For example: if text file contains 5 'a' items, the 5th 'a' item will be deleted.",background = "#89cff0")
        lbl8.grid(row = 4, column = 0, columnspan = 8, sticky = W)
        
        











        
        
    if (picked ==3):
        window.destroy()

        

        

def main_menu():

    
    global lbl1, rad1, rad2, rad3,btn1
    
    text1 = '*'*50
    text2 = '*'+' '*75 + '*'
    text3 = "*      Welcome to Sam's concentration game       *"
    text4 = (text1 + '\n' + text2 + '\n'  + text3 + '\n'  + text2 + '\n' + text1)
    lbl1 = tk.Label(window, text = text4, bg = "#89cff0")
    lbl1.grid(column = 1, row = 0, padx = 125)

    global selected
    selected = IntVar()
    selected.set(1)
    mycolour = "#89cff0"

    global selected_dif
    selected_dif = IntVar()
    selected_dif.set(6)
    rad1 = tk.Radiobutton(window, text = 'Play Game', value = 1, variable = selected, background = mycolour)
    rad2 = tk.Radiobutton(window, text = 'Enter Developer Mode', value = 2, variable = selected, background = mycolour)
    rad3 = tk.Radiobutton(window, text = 'Exit the Program', value = 3, variable = selected, background = mycolour)

    rad1.grid(column = 1, row = 5, padx = 195, sticky = W)
    rad2.grid(column = 1, row = 6, padx = 195, sticky = W)
    rad3.grid(column = 1, row = 7, padx = 195,sticky = W)


    btn1 = Button(window, text = "Enter",  command = clicked)
    btn1.grid(column = 1, row = 8, padx = 195, sticky = W)

    

window = Tk()
window.grid()
window.title("Welcome")
window.geometry('620x400')
window.resizable(width = False, height = True)
window.configure(bg = "#89cff0")
main_menu()
trial_num = 0





window.mainloop()
