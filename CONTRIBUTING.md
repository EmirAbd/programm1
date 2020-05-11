import telebot

bot = telebot.TeleBot("1255838288:AAHAfNr1a3EHIWwTM0BHhowEeMqU1ALAPec")

@bot.message_handler(commands=['start'])
def send_welcome(message):
    bot.reply_to(message,
                 "Привет я бот Азамата! Хочешь чтоб я помог тебе с распределением ролей в мафии пиши имя и я дам ему роль.")

bot.polling(none_stop=True)
