from telegram import Update
from telegram.ext import Updater, CommandHandler, CallbackContext

# Список заблокированных пользователей
blocked_users = set()

def start(update: Update, context: CallbackContext) -> None:
    update.message.reply_text('Привет! Я бот, который может блокировать пользователей и назначать мут.')

def block_user(update: Update, context: CallbackContext) -> None:
    if context.args:
        user_id = context.args[0]
        blocked_users.add(user_id)
        update.message.reply_text(f'Пользователь {user_id} заблокирован.')
    else:
        update.message.reply_text('Укажите ID пользователя для блокировки.')

def mute_user(update: Update, context: CallbackContext) -> None:
    if context.args:
        user_id = context.args[0]
        # Здесь можно реализовать логику для назначения мута, например, игнорировать сообщения от этого пользователя
        update.message.reply_text(f'Пользователь {user_id} получает мут.')
    else:
        update.message.reply_text('Укажите ID пользователя для назначения мута.')

def main() -> None:
    updater = Updater("7515881723:AAFTpGzyhevEHAB5gTpOTVGf-8YcU0TNCUI")

    dispatcher = updater.dispatcher

    dispatcher.add_handler(CommandHandler("start", start))
    dispatcher.add_handler(CommandHandler("block", block_user))
    dispatcher.add_handler(CommandHandler("mute", mute_user))

    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
