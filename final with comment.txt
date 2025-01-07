
; You may customize this and other start-up templates; 
; The location of this template is c:\emu8086\inc\0_com_template.txt

org 100h

org 100h

.model small 

.stack 100h

.data

header DB "- Library Application -",0Dh,0Ah
       DB "*************************",'$' 
       
NEWLINE    DB 10,13,"$"
      
menu       DB 0Dh,0Ah,0Dh,0Ah,"1- Display Books in library.",0Dh,0Ah
           DB "2- Add book.",0Dh,0Ah 
           DB "3- Remove book.",0Dh,0Ah
           DB "4- Display Members in library.",0Dh,0Ah
           DB "5- Add member.",0Dh,0Ah 
           DB "6- Remove member.",0Dh,0Ah
           DB "7- Display Order in library",0Dh,0Ah
           DB "8- Add order.",0Dh,0Ah
           DB "9- Remove order.",0Dh,0Ah
           DB "0- Exit.",0Dh,0Ah,
           DB "Please enter your choice: ",'$'

book_name  DB 0Dh,0Ah,0Dh,0Ah,"Please write the book name (max 17 character) and press Enter: ",'$'

book_type  DB 0Dh,0Ah,"Please write the book writer (max 10 character) and press Enter: ",'$'

book_num   DB 0Dh,0Ah,0Dh,0Ah,"Please write the book number you want to remove and press Enter: ",'$'

book_list  DB 0Dh,0Ah,0Dh,0Ah,"The Book List (Max 9 books)",0Dh,0Ah
           DB 0Dh,0Ah,"No.   Book Name           Book WRITER",'$' 


mem_name  DB 0Dh,0Ah,0Dh,0Ah,"Please write your name (max 17 character) and press Enter: ",'$'

mem_last  DB 0Dh,0Ah,"Please write your last name (max 10 character) and press Enter: ",'$'

mem_num   DB 0Dh,0Ah,0Dh,0Ah,"Please write the member number you want to remove and press Enter: ",'$'

mem_list  DB 0Dh,0Ah,0Dh,0Ah,"The member List (Max 9 books)",0Dh,0Ah
           DB 0Dh,0Ah,"No.   Member Name           Member Lastname",'$' 
           
          
order_book  DB 0Dh,0Ah,0Dh,0Ah,"Please write the book name you want to reseve and press Enter: ",'$'

order_name  DB 0Dh,0Ah,"Please write the member last name who wants to order book and press Enter: ",'$'

order_num   DB 0Dh,0Ah,0Dh,0Ah,"Please write the book number you want to remove and press Enter: ",'$'

order_list  DB 0Dh,0Ah,0Dh,0Ah,"The order List (Max 9 books)",0Dh,0Ah
           DB 0Dh,0Ah,"No.   Book Name           Member LastName",'$' 

;================================================           
           
space      DB "     ",'$'     
  
error_msg  DB 0Dh,0Ah,"This number does not exist",0Dh,0Ah,'$'

full_msg   DB 0Dh,0Ah,"There is no place to add a new book, delete book first",0Dh,0Ah,'$' 

error_msgm  DB 0Dh,0Ah,"This number does not exist",0Dh,0Ah,'$'

full_msgm   DB 0Dh,0Ah,"There is no place to add a new member, delete member first",0Dh,0Ah,'$'

error_msgr  DB 0Dh,0Ah,"This number does not exist",0Dh,0Ah,'$'

full_msgr   DB 0Dh,0Ah,"There is no place to add a new order, delete order first",0Dh,0Ah,'$' 
;================================================
           
book1_name DB "  Anna Karenina   ",'$'
book2_name DB "  The Great Gatsby          ",'$'
book3_name DB "  Passage to India ",'$'
book4_name DB "  Invisible Man        ",'$'
book5_name DB "  Beloved      ",'$'
book6_name DB 17 dup('$')
book7_name DB 17 dup('$')
book8_name DB 17 dup('$')
book9_name DB 17 dup('$')

book1_type DB "  Mayer Inc",'$'
book2_type DB "  Scott Fitzgerald",'$'
book3_type DB "  Forster ",'$'
book4_type DB "  Ralph Ellison",'$'
book5_type DB "  Toni Morrison",'$'
book6_type DB 12 dup('$')
book7_type DB 12 dup('$')
book8_type DB 12 dup('$')
book9_type DB 12 dup('$')  


mem1_name DB "  Nazanin   ",'$'
mem2_name DB "  Nika          ",'$'
mem3_name DB "  Matin ",'$'
mem4_name DB "  Hawzhin        ",'$'
mem5_name DB "  Sanyar      ",'$'
mem6_name DB 17 dup('$')
mem7_name DB 17 dup('$')
mem8_name DB 17 dup('$')
mem9_name DB 17 dup('$')

mem1_last DB "  Pravizi",'$'
mem2_last DB "  Amanati",'$'
mem3_last DB "  Gholami",'$'
mem4_last DB "  Ozayri",'$'
mem5_last DB "  Ahmadi",'$'
mem6_last DB 12 dup('$')
mem7_last DB 12 dup('$')
mem8_last DB 12 dup('$')
mem9_last DB 12 dup('$') 


order1_book DB "  Anna Karenina   ",'$'
order2_book DB "  Passage to India ",'$'
order3_book DB "  Beloved      ",'$'
order4_book DB "  Jane Eyre          ",'$'
order5_book DB "  Invisible Man        ",'$'
order6_book DB 17 dup('$')
order7_book DB 17 dup('$')
order8_book DB 17 dup('$')
order9_book DB 17 dup('$')

order1_name DB "  Pravizi",'$'
order2_name DB "  Amanati",'$'
order3_name DB "  Gholami",'$'
order4_name DB "  Ozayri",'$'
order5_name DB "  Ahmadi",'$'
order6_name DB 12 dup('$')
order7_name DB 12 dup('$')
order8_name DB 12 dup('$')
order9_name DB 12 dup('$')
                                                 
;================================================

available_book DB 1, 2, 3, 4, 5 ,0, 0, 0, 0
area       DD 0
operation  DB 0

available_mem DB 1, 2, 3, 4, 5 ,0, 0, 0, 0
aream       DD 0
operationm  DB 0 

available_order DB 1, 2, 3, 4, 5 ,0, 0, 0, 0
arear       DD 0
operationr  DB 0

;================================================ 
		                                  
.code

begin:
      ;Setting the address of the data piece
      mov ax,@data
      mov ds,ax

      ; print message for the header
      MOV AH,09H
      LEA DX,header
      INT 21H
      ; go to NEWLINE
      MOV AH,09H
      LEA DX,NEWLINE
      INT 21H

;================================================ 

  start:
      
      ;code to choose one choice from the menu
      MOV AH,09H
      LEA DX, menu
      INT 21H

get_choice:
      ; read the user choice
      mov ah, 1
      int 21h

      ; first choice
      cmp al, '1'
      je  FIRST_CHOICE
      
      ; second choice
      cmp al, '2'
      je  SECOND_CHOICE
      
      ; third choice
      cmp al, '3'
      je  THIRD_CHOICE
      
      ; forth choice
      cmp al, '4'
      je  FORTH_CHOICE
      
      ; fifth choice
      cmp al, '5'
      je  FIFTH_CHOICE
      
      ; sixth choice
      cmp al, '6'
      je  SIXTH_CHOICE

      ; seventh choice
      cmp al, '7'
      je  SEVENTH_CHOICE 
      
      ; eighth choice
      cmp al, '8'
      je  EIGHTH_CHOICE
      
      ; ninth choice
      cmp al, '9'
      je  NINTH_CHOICE
      
      ; zero choice
      cmp al, '0'
      je  ZERO_CHOICE
      
      ; loop back to get_choice until the user choose
      jmp get_choice
;BOOK================================================ 

FIRST_CHOICE:
      ; print raduis msg
      MOV AH,09H
      LEA DX, book_list
      INT 21H

      lea si, available_book
      mov bl, 0
      
  print_book:
      inc bl  ; book counter
      
      mov al, [si]
      inc si
      cmp al, 0  ; go to next book
      je next_book
      cmp al, 1  ; go to book 1
      je book1
      cmp al, 2  ; go to book 2
      je book2
      cmp al, 3  ; go to book 3
      je book3
      cmp al, 4  ; go to book 4
      je book4
      cmp al, 5  ; go to book 5
      je book5
      cmp al, 6  ; go to book 6
      je book6
      cmp al, 7  ; go to book 7
      je book7
      cmp al, 8  ; go to book 8
      je book8
      cmp al, 9  ; go to book 9
      je book9
      
      
    book1:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print book number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book1_name
      MOV AH,09H
      LEA DX, book1_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book1_type
      MOV AH,09H
      LEA DX, book1_type
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_book   
      
    book2: 
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print book number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book2_name
      MOV AH,09H
      LEA DX, book2_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book2_type
      MOV AH,09H
      LEA DX, book2_type
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_book  
      
    book3: 
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print book number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book3_name
      MOV AH,09H
      LEA DX, book3_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book3_type
      MOV AH,09H
      LEA DX, book3_type
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_book  
      
    book4: 
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print book number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book4_name
      MOV AH,09H
      LEA DX, book4_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book4_type
      MOV AH,09H
      LEA DX, book4_type
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_book  
      
    book5: 
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print book number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book5_name
      MOV AH,09H
      LEA DX, book5_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book5_type
      MOV AH,09H
      LEA DX, book5_type
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_book  
      
    book6: 
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print book number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book6_name
      MOV AH,09H
      LEA DX, book6_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book6_type
      MOV AH,09H
      LEA DX, book6_type
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_book  
      
    book7: 
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print book number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book7_name
      MOV AH,09H
      LEA DX, book7_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book7_type
      MOV AH,09H
      LEA DX, book7_type
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_book  
      
    book8: 
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print book number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book8_name
      MOV AH,09H
      LEA DX, book8_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book8_type
      MOV AH,09H
      LEA DX, book8_type
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_book  
      
    book9: 
       ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print book number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book9_name
      MOV AH,09H
      LEA DX, book9_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print book9_type
      MOV AH,09H
      LEA DX, book9_type
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H       
      
      jmp next_book

  next_book:
    cmp bl, 9
    jg start
    jmp print_book

;================================================ 
      
SECOND_CHOICE:
  
      lea si, available_book
      mov bl, 0
       
  add_book:
      ; check for empty place
      mov al, [si]
      inc si
      inc bl  ; book counter
      cmp bl, 9
      jg full_place  ; if bl==9 there is no place to add a new book
      cmp al, 0  ; if al==0 there is empty place
      je found_place
      jmp add_book
      
  found_place:
      dec si
      mov [si], bl  ; save the book num in the list
      mov al, bl  ; al now have the number of the empty place to add the book
      cmp al, 1  ; add book at place 1
      je add_book1
      cmp al, 2  ; add book at place 2
      je add_book2
      cmp al, 3  ; add book at place 3
      je add_book3
      cmp al, 4  ; add book at place 4
      je add_book4
      cmp al, 5  ; add book at place 5
      je add_book5
      cmp al, 6  ; add book at place 6
      je add_book6
      cmp al, 7  ; add book at place 7
      je add_book7
      cmp al, 8  ; add book at place 8
      je add_book8
      cmp al, 9  ; add book at place 9
      je add_book9 

    ; add book in place 1
    add_book1:
      ; print book_name msg
      MOV AH,09H
      LEA DX, book_name
      INT 21H
      ; Get the book name
      mov ah,0ah
      lea dx, book1_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print book_type msg
      MOV AH,09H
      LEA DX, book_type
      INT 21H       
      ; Get the book type
      mov ah,0ah
      lea dx, book1_type
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
    
    ; add book in place 2    
    add_book2:
      ; print book_name msg
      MOV AH,09H
      LEA DX, book_name
      INT 21H
      ; Get the book name
      mov ah,0ah
      lea dx, book2_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print book_type msg
      MOV AH,09H
      LEA DX, book_type
      INT 21H       
      ; Get the book type
      mov ah,0ah
      lea dx, book2_type
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad

    ; add book in place 3 
    add_book3:
      ; print book_name msg
      MOV AH,09H
      LEA DX, book_name
      INT 21H
      ; Get the book name
      mov ah,0ah
      lea dx, book3_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print book_type msg
      MOV AH,09H
      LEA DX, book_type
      INT 21H       
      ; Get the book type
      mov ah,0ah
      lea dx, book3_type
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add book in place 4 
    add_book4:
      ; print book_name msg
      MOV AH,09H
      LEA DX, book_name
      INT 21H
      ; Get the book name
      mov ah,0ah
      lea dx, book4_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print book_type msg
      MOV AH,09H
      LEA DX, book_type
      INT 21H       
      ; Get the book type
      mov ah,0ah
      lea dx, book4_type
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add book in place 5 
    add_book5:
      ; print book_name msg
      MOV AH,09H
      LEA DX, book_name
      INT 21H
      ; Get the book name
      mov ah,0ah
      lea dx, book5_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print book_type msg
      MOV AH,09H
      LEA DX, book_type
      INT 21H       
      ; Get the book type
      mov ah,0ah
      lea dx, book5_type
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add book in place 6 
    add_book6:
      ; print book_name msg
      MOV AH,09H
      LEA DX, book_name
      INT 21H
      ; Get the book name
      mov ah,0ah
      lea dx, book6_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print book_type msg
      MOV AH,09H
      LEA DX, book_type
      INT 21H       
      ; Get the book type
      mov ah,0ah
      lea dx, book6_type
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add book in place 7 
    add_book7:
      ; print book_name msg
      MOV AH,09H
      LEA DX, book_name
      INT 21H
      ; Get the book name
      mov ah,0ah
      lea dx, book7_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print book_type msg
      MOV AH,09H
      LEA DX, book_type
      INT 21H       
      ; Get the book type
      mov ah,0ah
      lea dx, book7_type
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add book in place 8 
    add_book8:
      ; print book_name msg
      MOV AH,09H
      LEA DX, book_name
      INT 21H
      ; Get the book name
      mov ah,0ah
      lea dx, book8_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print book_type msg
      MOV AH,09H
      LEA DX, book_type
      INT 21H       
      ; Get the book type
      mov ah,0ah
      lea dx, book8_type
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad

    ; add book in place 9 
    add_book9:
      ; print book_name msg
      MOV AH,09H
      LEA DX, book_name
      INT 21H
      ; Get the book name
      mov ah,0ah
      lea dx, book9_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print book_type msg
      MOV AH,09H
      LEA DX, book_type
      INT 21H       
      ; Get the book type
      mov ah,0ah
      lea dx, book9_type
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
  
  ; when there is no space for new book  
  full_place:
      ; print full_msg
      MOV AH,09H
      LEA DX, full_msg
      INT 21H
      jmp start
      
  ; fill the rest of the name with space for printing
  space_pad:
    mov ax, 0
    mov cx, 0
    mov al, [si+1]  ; get the length of the string
    add al, 2       ; for the buffer size  
    mov cl, 17
    sub cl, al      ; initilaize the counter
    add ax, si      
    mov si, ax      ; go to character after the last character
    space_loop:
      mov [si], 32  ; add space to the name
      inc si
    loop space_loop
    
    ; add $ to the end of the book type string
    mov ax, 0
    mov cx, 0
    mov al, [di+1]  ; get the length of the string
    add al, 2       ; for the buffer size  
    add ax, di      
    mov di, ax      ; go to character after the last character
    mov [di], '$'   ; add $ to the end        
    
    jmp start 
;================================================ 
      
THIRD_CHOICE:
      ; print book_num msg
      mov ah,09h
      lea dx, book_num
      int 21h
      ; read the user choice
      mov ah, 1
      int 21h
      sub al, 48
       
      lea si, available_book
      mov bl, 0
      
      ; check for book
    check_book:
      cmp al, [si]
      je found_book
      inc si
      inc bl  ; book counter
      cmp bl, 9
      jg wrong  ; the book number does not exist
      jmp check_book      
    
  found_book:
      mov [si], 0
      
      jmp start
  
  wrong:
      ; print error_msg
      MOV AH,09H
      LEA DX, error_msg
      INT 21H    
      
      jmp start
;MEMBER================================================ 

FORTH_CHOICE:
      ; print raduis msg
      MOV AH,09H
      LEA DX, mem_list
      INT 21H

      lea si, available_mem
      mov bl, 0
      
  print_mem:
      inc bl  ; member counter
      
      mov al, [si]
      inc si
      cmp al, 0  ; go to next member
      je next_mem
      cmp al, 1  ; go to mem 1
      je mem1
      cmp al, 2  ; go to mem 2
      je mem2
      cmp al, 3  ; go to mem 3
      je mem3
      cmp al, 4  ; go to mem 4
      je mem4
      cmp al, 5  ; go to mem 5
      je mem5
      cmp al, 6  ; go to mem 6
      je mem6
      cmp al, 7  ; go to mem 7
      je mem7
      cmp al, 8  ; go to mem 8
      je mem8
      cmp al, 9  ; go to mem 9
      je mem9
      
      
    mem1:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print mem number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem1_name
      MOV AH,09H
      LEA DX, mem1_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem1_last
      MOV AH,09H
      LEA DX, mem1_last
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_mem  
      
    mem2:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print mem number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem2_name
      MOV AH,09H
      LEA DX, mem2_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem2_last
      MOV AH,09H
      LEA DX, mem2_last
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_mem
      
    mem3:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print mem number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem3_name
      MOV AH,09H
      LEA DX, mem3_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem3_last
      MOV AH,09H
      LEA DX, mem3_last
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_mem  
      
    mem4:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print mem number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem4_name
      MOV AH,09H
      LEA DX, mem4_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem4_last
      MOV AH,09H
      LEA DX, mem4_last
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_mem
      
    mem5:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print mem number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem5_name
      MOV AH,09H
      LEA DX, mem5_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem5_last
      MOV AH,09H
      LEA DX, mem5_last
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_mem 
      
     mem6:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print mem number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem6_name
      MOV AH,09H
      LEA DX, mem6_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem6_last
      MOV AH,09H
      LEA DX, mem6_last
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_mem
      
    mem7:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print mem number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem7_name
      MOV AH,09H
      LEA DX, mem7_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem7_last
      MOV AH,09H
      LEA DX, mem7_last
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_mem
      
    mem8:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print mem number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem8_name
      MOV AH,09H
      LEA DX, mem8_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem8_last
      MOV AH,09H
      LEA DX, mem8_last
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_mem
      
    mem9: 
       ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print mem number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem9_name
      MOV AH,09H
      LEA DX, mem9_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print mem9_last
      MOV AH,09H
      LEA DX, mem9_last
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_mem  
      
  next_mem:
    cmp bl, 9
    jg start
    jmp print_mem
              
     
;================================================

FIFTH_CHOICE:
  
      lea si, available_mem
      mov bl, 0
       
  add_mem:
      ; check for empty place
      mov al, [si]
      inc si
      inc bl  ; mem counter
      cmp bl, 9
      jg full_placemem  ; there is no place to add a new mem
      cmp al, 0  ; there is empty place
      je found_placemem
      jmp add_mem
      
  found_placemem:
      dec si
      mov [si], bl  ; save the member num in the list
      mov al, bl  ; al now have the number of the empty place to add the member
      cmp al, 1  ; add mem at place 1
      je add_mem1
      cmp al, 2  ; add mem at place 2
      je add_mem2
      cmp al, 3  ; add mem at place 3
      je add_mem3
      cmp al, 4  ; add mem at place 4
      je add_mem4
      cmp al, 5  ; add mem at place 5
      je add_mem5
      cmp al, 6  ; add mem at place 6
      je add_mem6
      cmp al, 7  ; add mem at place 7
      je add_mem7
      cmp al, 8  ; add mem at place 8
      je add_mem8
      cmp al, 9  ; add mem at place 9
      je add_mem9 

    ; add mem in place 1
    add_mem1:
      ; print mem_name msg
      MOV AH,09H
      LEA DX, mem_name
      INT 21H
      ; Get the mem name
      mov ah,0ah
      lea dx, mem1_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print mem_last msg
      MOV AH,09H
      LEA DX, mem_last
      INT 21H       
      ; Get the mem last
      mov ah,0ah
      lea dx, mem1_last
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad  
      
    ; add mem in place 2
    add_mem2:
      ; print mem_name msg
      MOV AH,09H
      LEA DX, mem_name
      INT 21H
      ; Get the mem name
      mov ah,0ah
      lea dx, mem2_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print mem_last msg
      MOV AH,09H
      LEA DX, mem_last
      INT 21H       
      ; Get the mem last
      mov ah,0ah
      lea dx, mem2_last
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad 
      
    ; add mem in place 3
    add_mem3:
      ; print mem_name msg
      MOV AH,09H
      LEA DX, mem_name
      INT 21H
      ; Get the mem name
      mov ah,0ah
      lea dx, mem3_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print mem_last msg
      MOV AH,09H
      LEA DX, mem_last
      INT 21H       
      ; Get the mem last
      mov ah,0ah
      lea dx, mem3_last
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
       
    ; add mem in place 4
    add_mem4:
      ; print mem_name msg
      MOV AH,09H
      LEA DX, mem_name
      INT 21H
      ; Get the mem name
      mov ah,0ah
      lea dx, mem4_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print mem_last msg
      MOV AH,09H
      LEA DX, mem_last
      INT 21H       
      ; Get the mem last
      mov ah,0ah
      lea dx, mem4_last
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add mem in place 5
    add_mem5:
      ; print mem_name msg
      MOV AH,09H
      LEA DX, mem_name
      INT 21H
      ; Get the mem name
      mov ah,0ah
      lea dx, mem5_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print mem_last msg
      MOV AH,09H
      LEA DX, mem_last
      INT 21H       
      ; Get the mem last
      mov ah,0ah
      lea dx, mem5_last
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad    
                   
    ; add mem in place 6
    add_mem6:
      ; print mem_name msg
      MOV AH,09H
      LEA DX, mem_name
      INT 21H
      ; Get the mem name
      mov ah,0ah
      lea dx, mem6_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print mem_last msg
      MOV AH,09H
      LEA DX, mem_last
      INT 21H       
      ; Get the mem last
      mov ah,0ah
      lea dx, mem6_last
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add mem in place 7
    add_mem7:
      ; print mem_name msg
      MOV AH,09H
      LEA DX, mem_name
      INT 21H
      ; Get the mem name
      mov ah,0ah
      lea dx, mem7_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print mem_last msg
      MOV AH,09H
      LEA DX, mem_last
      INT 21H       
      ; Get the mem last
      mov ah,0ah
      lea dx, mem7_last
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad 
      
    ; add mem in place 8
    add_mem8:
      ; print mem_name msg
      MOV AH,09H
      LEA DX, mem_name
      INT 21H
      ; Get the mem name
      mov ah,0ah
      lea dx, mem8_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print mem_last msg
      MOV AH,09H
      LEA DX, mem_last
      INT 21H       
      ; Get the mem last
      mov ah,0ah
      lea dx, mem8_last
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad 
      
    ; add mem in place 9
    add_mem9:
      ; print mem_name msg
      MOV AH,09H
      LEA DX, mem_name
      INT 21H
      ; Get the mem name
      mov ah,0ah
      lea dx, mem9_name
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print mem_last msg
      MOV AH,09H
      LEA DX, mem_last
      INT 21H       
      ; Get the mem last
      mov ah,0ah
      lea dx, mem9_last
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
  ; when there is no space for new member  
  full_placemem:
      ; print full_msgm
      MOV AH,09H
      LEA DX, full_msgm
      INT 21H
      jmp start
      
  ; fill the rest of the name with space for printing
  space_padmem:
    mov ax, 0
    mov cx, 0
    mov al, [si+1]  ; get the length of the string
    add al, 2       ; for the buffer size  
    mov cl, 17
    sub cl, al      ; initilaize the counter
    add ax, si      
    mov si, ax      ; go to character after the last character
    space_loopmem:
      mov [si], 32  ; add space to the name
      inc si
    loop space_loop
    
    ; add $ to the end of the book type string
    mov ax, 0
    mov cx, 0
    mov al, [di+1]  ; get the length of the string
    add al, 2       ; for the buffer size  
    add ax, di      
    mov di, ax      ; go to character after the last character
    mov [di], '$'   ; add $ to the end        
    
    jmp start 
;================================================ 

SIXTH_CHOICE:
      ; print mem_num msg
      mov ah,09h
      lea dx, mem_num
      int 21h
      ; read the user choice
      mov ah, 1
      int 21h
      sub al, 48
       
      lea si, available_mem
      mov bl, 0
      
    ; check for mem
    check_mem:
      cmp al, [si]
      je found_mem
      inc si
      inc bl  ; mem counter
      cmp bl, 9
      jg wrong  ; the member number does not exist
      jmp check_mem      
    
  found_mem:
      mov [si], 0
      
      jmp start
  
  wrongmem:
      ; print error_msgm
      MOV AH,09H
      LEA DX, error_msgm
      INT 21H     
      
      jmp start                  
;ORDER================================================

SEVENTH_CHOICE:
      ; print raduis msg
      MOV AH,09H
      LEA DX, order_list
      INT 21H

      lea si, available_order
      mov bl, 0
      
  print_order:
      inc bl  ; order counter
      
      mov al, [si]
      inc si
      cmp al, 0  ; go to next order
      je next_order
      cmp al, 1  ; go to order 1
      je order1
      cmp al, 2  ; go to order 2
      je order2
      cmp al, 3  ; go to order 3
      je order3
      cmp al, 4  ; go to order 4
      je order4
      cmp al, 5  ; go to order 5
      je order5
      cmp al, 6  ; go to order 6
      je order6
      cmp al, 7  ; go to order 7
      je order7
      cmp al, 8  ; go to order 8
      je order8
      cmp al, 9  ; go to order 9
      je order9
      
      
    order1:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print order number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order1_book
      MOV AH,09H
      LEA DX, order1_book
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order1_name
      MOV AH,09H
      LEA DX, order1_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_order
      
    order2:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print order number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order2_book
      MOV AH,09H
      LEA DX, order2_book
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order2_name
      MOV AH,09H
      LEA DX, order2_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_order
      
    order3:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print order number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order3_book
      MOV AH,09H
      LEA DX, order3_book
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order3_name
      MOV AH,09H
      LEA DX, order3_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_order
      
    order4:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print order number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order4_book
      MOV AH,09H
      LEA DX, order4_book
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order4_name
      MOV AH,09H
      LEA DX, order4_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_order 
      
    order5:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print order number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order5_book
      MOV AH,09H
      LEA DX, order5_book
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order5_name
      MOV AH,09H
      LEA DX, order5_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_order
      
    order6:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print order number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order6_book
      MOV AH,09H
      LEA DX, order6_book
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order6_name
      MOV AH,09H
      LEA DX, order6_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_order 
      
    order7:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print order number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order7_book
      MOV AH,09H
      LEA DX, order7_book
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order7_name
      MOV AH,09H
      LEA DX, order7_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_order
      
    order8:
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print order number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order8_book
      MOV AH,09H
      LEA DX, order8_book
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order8_name
      MOV AH,09H
      LEA DX, order8_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_order
      
    order9: 
      ; print new line
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H    
      ; print order number
      MOV AH,02H
      MOV Dl, bl
      add Dl, 48
      INT 21H
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order9_book
      MOV AH,09H
      LEA DX, order9_book
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H   
      ; print space
      MOV AH,09H
      LEA DX, space
      INT 21H 
      ; print order9_name
      MOV AH,09H
      LEA DX, order9_name
      add dx,02h          ; to get rid of the space on the beginning or the buffer size
      INT 21H     
      
      jmp next_order  
      
  next_order:
    cmp bl, 9
    jg start
    jmp print_order  
 
;================================================

EIGHTH_CHOICE:
  
      lea si, available_order
      mov bl, 0
       
  add_order:
      ; check for empty place
      mov al, [si]
      inc si
      inc bl  ; order counter
      cmp bl, 9
      jg full_placer  ; there is no place to add a new order
      cmp al, 0  ; there is empty place
      je found_placer
      jmp add_order
      
  found_placer:
      dec si
      mov [si], bl  ; save the order num in the list
      mov al, bl  ; al now have the number of the empty place to add the order
      cmp al, 1  ; add order at place 1
      je add_order1
      cmp al, 2  ; add order at place 2
      je add_order2
      cmp al, 3  ; add order at place 3
      je add_order3
      cmp al, 4  ; add order at place 4
      je add_order4
      cmp al, 5  ; add order at place 5
      je add_order5
      cmp al, 6  ; add order at place 6
      je add_order6
      cmp al, 7  ; add order at place 7
      je add_order7
      cmp al, 8  ; add order at place 8
      je add_order8
      cmp al, 9  ; add order at place 9
      je add_order9 

    ; add order in place 1
    add_order1:
      ; print order_book msg
      MOV AH,09H
      LEA DX, order_book
      INT 21H
      ; Get the order book
      mov ah,0ah
      lea dx, order1_book
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print order_name msg
      MOV AH,09H
      LEA DX, order_name
      INT 21H       
      ; Get the order name
      mov ah,0ah
      lea dx, order1_name
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad 
      
    ; add order in place 2
    add_order2:
      ; print order_book msg
      MOV AH,09H
      LEA DX, order_book
      INT 21H
      ; Get the order book
      mov ah,0ah
      lea dx, order2_book
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print order_name msg
      MOV AH,09H
      LEA DX, order_name
      INT 21H       
      ; Get the order name
      mov ah,0ah
      lea dx, order2_name
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add order in place 3
    add_order3:
      ; print order_book msg
      MOV AH,09H
      LEA DX, order_book
      INT 21H
      ; Get the order book
      mov ah,0ah
      lea dx, order3_book
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print order_name msg
      MOV AH,09H
      LEA DX, order_name
      INT 21H       
      ; Get the order name
      mov ah,0ah
      lea dx, order3_name
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add order in place 4
    add_order4:
      ; print order_book msg
      MOV AH,09H
      LEA DX, order_book
      INT 21H
      ; Get the order book
      mov ah,0ah
      lea dx, order4_book
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print order_name msg
      MOV AH,09H
      LEA DX, order_name
      INT 21H       
      ; Get the order name
      mov ah,0ah
      lea dx, order4_name
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add order in place 5
    add_order5:
      ; print order_book msg
      MOV AH,09H
      LEA DX, order_book
      INT 21H
      ; Get the order book
      mov ah,0ah
      lea dx, order5_book
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print order_name msg
      MOV AH,09H
      LEA DX, order_name
      INT 21H       
      ; Get the order name
      mov ah,0ah
      lea dx, order5_name
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add order in place 6
    add_order6:
      ; print order_book msg
      MOV AH,09H
      LEA DX, order_book
      INT 21H
      ; Get the order book
      mov ah,0ah
      lea dx, order6_book
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print order_name msg
      MOV AH,09H
      LEA DX, order_name
      INT 21H       
      ; Get the order name
      mov ah,0ah
      lea dx, order6_name
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad  
      
    ; add order in place 7
    add_order7:
      ; print order_book msg
      MOV AH,09H
      LEA DX, order_book
      INT 21H
      ; Get the order book
      mov ah,0ah
      lea dx, order7_book
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print order_name msg
      MOV AH,09H
      LEA DX, order_name
      INT 21H       
      ; Get the order name
      mov ah,0ah
      lea dx, order7_name
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add order in place 8
    add_order8:
      ; print order_book msg
      MOV AH,09H
      LEA DX, order_book
      INT 21H
      ; Get the order book
      mov ah,0ah
      lea dx, order8_book
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print order_name msg
      MOV AH,09H
      LEA DX, order_name
      INT 21H       
      ; Get the order name
      mov ah,0ah
      lea dx, order8_name
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad
      
    ; add order in place 9
    add_order9:
      ; print order_book msg
      MOV AH,09H
      LEA DX, order_book
      INT 21H
      ; Get the order book
      mov ah,0ah
      lea dx, order9_book
      int 21h 
      mov si, dx   ; save the address for space padding
      
      ; print NEWLINE
      MOV AH,09H
      LEA DX, NEWLINE
      INT 21H
      
      ; print order_name msg
      MOV AH,09H
      LEA DX, order_name
      INT 21H       
      ; Get the order name
      mov ah,0ah
      lea dx, order9_name
      int 21h 
      mov di, dx   ; save the address for end string
      jmp space_pad

  ; when there is no space for new order  
  full_placer:
      ; print full_msgr
      MOV AH,09H
      LEA DX, full_msgr
      INT 21H
      jmp start
      
  ; fill the rest of the name with space for printing
  space_padr:
    mov ax, 0
    mov cx, 0
    mov al, [si+1]  ; get the length of the string
    add al, 2       ; for the buffer size  
    mov cl, 17
    sub cl, al      ; initilaize the counter
    add ax, si      
    mov si, ax      ; go to character after the last character
    space_loopr:
      mov [si], 32  ; add space to the name
      inc si
    loop space_loopr
    
    ; add $ to the end of the book type string
    mov ax, 0
    mov cx, 0
    mov al, [di+1]  ; get the length of the string
    add al, 2       ; for the buffer size  
    add ax, di      
    mov di, ax      ; go to character after the last character
    mov [di], '$'   ; add $ to the end        
    
    jmp start
       
;================================================

NINTH_CHOICE:
      ; print order_num msg
      mov ah,09h
      lea dx, order_num
      int 21h
      ; read the user choice
      mov ah, 1
      int 21h
      sub al, 48
       
      lea si, available_order
      mov bl, 0
      
    ; check for order
    check_order:
      cmp al, [si]
      je found_order
      inc si
      inc bl  ; order counter
      cmp bl, 9
      jg wrong  ; the order number does not exist
      jmp check_order      
    
  found_order:
      mov [si], 0
      
      jmp start
  
  wrongr:
      ; print error_msgr
      MOV AH,09H
      LEA DX, error_msgr
      INT 21H    
      
      jmp start
      
;================================================
ZERO_CHOICE:

      mov ah,0Ch
      int 21h 

ret



;-----------------------------------------