import telebot
from telebot import types

from requests import get

bot = telebot.TeleBot("1255838288:AAHAfNr1a3EHIWwTM0BHhowEeMqU1ALAPec")

# кнопка "начать"
markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
item1 = types.KeyboardButton("go")
markup.add(item1)


@bot.message_handler(commands=['start'])
def send_welcome(message):
    bot.send_message(message.chat.id,
                     "Добро пожаловать, {0.first_name}!\nЯ - <b>{1.first_name}</b>,".format(
                         message.from_user, bot.get_me()),
                     parse_mode='html', reply_markup=markup)

@bot.message_handler(content_types=['text'])
def start(message):
    if message.text == "go":
        keyboard = types.InlineKeyboardMarkup();  # наша клавиатура
        key_yes = types.InlineKeyboardButton(text='правильно', callback_data='yes');  # кнопка «Да»
        keyboard.add(key_yes);  # добавляем кнопку в клавиатуру
        key_no = types.InlineKeyboardButton(text='неправильно', callback_data='no');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='неправильно', callback_data='no');
        keyboard.add(key_no);
        key_no = types.InlineKeyboardButton(text='неправильно', callback_data='no');
        keyboard.add(key_no);

        bot.send_message(message.from_user.id, "кто это", reply_markup=keyboard)

    else:
        bot.send_message(message.from_user.id, 'Нажми на кнопку');


@bot.callback_query_handler(func=lambda call: True)
def callback_worker(call):
    if call.data == "yes":
        bot.send_message(call.message.chat.id, 'Молодец : )');
    elif call.data == "no":
        bot.send_message(call.message.chat.id, "Не угадал, попробуй еще раз", )


bot.polling(none_stop=True, interval=0)

