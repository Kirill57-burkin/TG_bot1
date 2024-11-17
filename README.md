import random
import telebot
import os
from telebot.types import Message
bot = telebot.TeleBot('7830680162:AAGBQ75NbcDJ-dO03Ae-9imguFLD7ecedio')
@bot.message_handler(commands=['start'])
def comman_start(message:Message):
    bot.reply_to(message,'hi, I am school bot')

@bot.message_handler(commands=['coins'])
def cmd_coins(message: Message):
    x = random.randint(1, 2)
    if x == 1:
        bot.reply_to(message, 'Выпал орел🦅')
    else:
        bot.reply_to(message, 'Выпала решка🙁')

@bot.message_handler(commands=['match'])
def comman_match(message:Message):
    match=message.text
    bot.reply_to(message,'2+2=4')
@bot.message_handler(commands=['English'])
def comman_engl(message:Message):
    bot.reply_to(message,'London is the capital of Britan')

@bot.message_handler(commands=['physic'])
def comman_phy(message:Message):
    bot.reply_to(message,'Enstain is the most populat phyisicman')
@bot.message_handler(commands=['password'])
def comman_phy(message:Message):
    glas='eyuioaEYUIOA'
    sogl='qwrtpsdfghjklzxcvbnmQWRTPSDFGHJKLZXCVBNM'
    numbers='0123456789'
    digitals='!@#$%'
    password=''
    for i in range(random.randint(3, 4)):
        password +=random.choice(sogl) + random.choice(glas)
    for i in range(random.randint(3, 4)):
        password +=random.choice(numbers) + random.choice(digitals)
    bot.reply_to(message, password)
@bot.message_handler(commands=['name'])
def cmd_name(message:Message):
    bot.reply_to(message,'What is your name?')
    bot.register_next_step_handler(message, get_name)
def get_name(message: Message):
    name = message.text
    bot.reply_to(message,'Ваше имя'+ name)
@bot.message_handler(commands=['knd'])
def cmd_name(message:Message):
    bot.reply_to(message,'what choice')
    bot.register_next_step_handler(message, get_knd)
def get_knd(message: Message):
    player = message.text
    comp = random.choice(['камень', 'ножницы', 'бумага'])
    if player == comp:
        bot.reply_to(message, 'Ничья!')
    elif player == 'камень' and comp == 'ножницы':
        bot.reply_to(message, 'Вы победили!')
    elif player == 'ножницы' and comp == 'бумага':
        bot.reply_to(message, 'Вы победили!')
    elif player == 'бумага' and comp == 'камень':
        bot.reply_to(message, 'Вы победили!')
    else:
        bot.reply_to(message, 'Вы проиграли!')

@bot.message_handler(commands=['riddle'])
def comman_riddle(message:Message):
    riddle_coice =['С хозяином дружит,Дом сторожит,Живёт под крылечком,А хвост колечком.','Гладишь - ласкается,Дразнишь - кусается.','Что за чудо-покрывало?Ночью все вдруг белым стало.Не видать дорог и рек -Их укрыл пушистый...']
    qqq = random.choice(riddle_coice)
    bot.reply_to(message, qqq)

@bot.message_handler(commands=['task'])
def cmd_task(message: Message):
    bot.reply_to(message, 'Какую задачу вы хотите добавить?')
    bot.register_next_step_handler(message, add_task)
def add_task(message: Message):
    task = message.text
    with open('tasks.txt','a', encoding='utf-8') as file:
        file.write(task +'\n')
        bot.reply_to(message,'+')


@bot.message_handler(commands=['read'])
def cmd_read(message: Message):
    with open('tasks.txt','r',encoding='utf-8') as file:
        text=file.read()
        bot.reply_to(message, text)

@bot.message_handler(commands=['mem'])
def cmd_mems(message: Message):
    mems=os.listdir('mem')
    mems=[
        'first_mem.jpg',
        'second_mem.jpg',
        'thre_mem.jpg'
        ]
    mem =random.choice(mems)
    mem ='mem/'+ mem
    with open(mem,'rb') as file:
        bot.send_photo(message.chat.id,file)



bot.polling()
