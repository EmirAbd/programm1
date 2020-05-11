import telebot
from telebot import types
import random

from requests import get

bot = telebot.TeleBot("1180765949:AAH4SSxWm4tcmvSCvMHsihBBbonVLMCV_Kg")





# кнопка "начать"
markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
item1 = types.KeyboardButton("go")
markup.add(item1)
queations = ['q1','q2','q3','q4','q5','q6']

@bot.message_handler(commands=['start'])
def send_welcome(message):
    bot.send_message(message.chat.id,
                     "Добро пожаловать, {0.first_name}!\nЯ - <b>{1.first_name}</b>,".format(
                         message.from_user, bot.get_me()),
                     parse_mode='html', reply_markup=markup)

@bot.message_handler(content_types=['text'])
def random1(message):
    r = random.choice(queations)
    if r == 'q1':


            keyboard = types.InlineKeyboardMarkup();  # наша клавиатура
            key_yes = types.InlineKeyboardButton(text='3.1415', callback_data='yes');  # кнопка «Да»
            keyboard.add(key_yes);  # добавляем кнопку в клавиатуру
            key_no = types.InlineKeyboardButton(text='3.1412', callback_data='no');
            keyboard.add(key_no);
            key_no = types.InlineKeyboardButton(text='3.1212', callback_data='no');
            keyboard.add(key_no);
            key_no = types.InlineKeyboardButton(text='3.1411', callback_data='no');
            keyboard.add(key_no);

            bot.send_message(message.from_user.id, "чему равно число пи?", reply_markup=keyboard)
    elif r == 'q2':

        keyboard = types.InlineKeyboardMarkup();  # наша клавиатура
        key_yes = types.InlineKeyboardButton(text='Саша Архангель', callback_data='no');  # кнопка «Да»
        keyboard.add(key_yes);  # добавляем кнопку в клавиатуру
        key_no = types.InlineKeyboardButton(text='Арнольд Маск', callback_data='no');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='X Æ A-12', callback_data='yes');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='X Ar A1 Маск', callback_data='no');
        keyboard.add(key_no);

        bot.send_message(message.from_user.id, "как зовут сына Илона Маска?", reply_markup=keyboard)
    elif r == 'q3':

        keyboard = types.InlineKeyboardMarkup();  # наша клавиатура
        key_yes = types.InlineKeyboardButton(text='1981', callback_data='no');  # кнопка «Да»
        keyboard.add(key_yes);  # добавляем кнопку в клавиатуру
        key_no = types.InlineKeyboardButton(text='1961', callback_data='yes');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='1951', callback_data='no');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='1970', callback_data='no');
        keyboard.add(key_no);

        bot.send_message(message.from_user.id, "в каком году Ю.Гагарин полетел в космос?", reply_markup=keyboard)
    elif r == 'q4':

        keyboard = types.InlineKeyboardMarkup();  # наша клавиатура
        key_yes = types.InlineKeyboardButton(text='Луна', callback_data='no');  # кнопка «Да»
        keyboard.add(key_yes);  # добавляем кнопку в клавиатуру
        key_no = types.InlineKeyboardButton(text='R12h1', callback_data='no');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='Титан', callback_data='no');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='Плутон', callback_data='yes');
        keyboard.add(key_no);

        bot.send_message(message.from_user.id, "какой астероит в нашей солничной системе раньше считался планетай?", reply_markup=keyboard)
    elif r == 'q5':

        keyboard = types.InlineKeyboardMarkup();  # наша клавиатура
        key_yes = types.InlineKeyboardButton(text='Стив Джобс', callback_data='no');  # кнопка «Да»
        keyboard.add(key_yes);  # добавляем кнопку в клавиатуру
        key_no = types.InlineKeyboardButton(text='Тим Кук', callback_data='yes');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='Стейн Метер', callback_data='no');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='Био Гейтс', callback_data='no');
        keyboard.add(key_no);

        bot.send_message(message.from_user.id, "как зовут нынешнего директора Apple?", reply_markup=keyboard)
    elif r == 'q6':

        keyboard = types.InlineKeyboardMarkup();  # наша клавиатура
        key_yes = types.InlineKeyboardButton(text='4', callback_data='no');  # кнопка «Да»
        keyboard.add(key_yes);  # добавляем кнопку в клавиатуру
        key_no = types.InlineKeyboardButton(text='6', callback_data='no');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='8', callback_data='no');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='10', callback_data='yes');
        keyboard.add(key_no);

        bot.send_message(message.from_user.id, "2+2*2^2", reply_markup=keyboard)




@bot.message_handler(content_types=['text'])
def start(message):
    if message.text == "go":
        return random1()



    else:
        bot.send_message(message.from_user.id, 'Нажми на кнопку');


@bot.callback_query_handler(func=lambda call: True)
def callback_worker(call):
    if call.data == "yes":
        bot.send_message(call.message.chat.id, 'Молодец : )')
      

    elif call.data == "no":
        bot.send_message(call.message.chat.id, "Не угадал, попробуй еще раз")


bot.polling(none_stop=True,interval=0)

