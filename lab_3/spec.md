# розглянуті UC - користування чатом

## UC-1 : користувач вирішив написати повідомлення в чаті трансляції

учасники :

- user
- charUI
- chatService
- message
- chat

Кроки:

1. enterText(text): написання повідомлення
2. sendReq(): натискання кнопки надіслати
3. postMes(status, text, us_id, stream_id, chat_id): запит на сервіс для обробки запиту надсилання повідомлення
4. checkLastMess(us_id): запит на отримання id останнього повідомлення користувача
5. return (lastMessId): повернення id останнього повідомлення користувача сервісу
6. takeLastMessParam(us_id, lastMessId) запит на отримання часу коли останнє повідомлення було записано
7. return(lastTime) отримання цього часу сервісом
8. audit(status, text, us_id, lastTime) перевірка на відповідність всім вимогам для надсилання повідомлення

ALT
auditstatus = err: (9-10)

9. return(audit_status): повернення статусу перевірки
10. postErrType(Err) відобарженя помилки із збереженим текстом та часом що залишилось почекати

auditstatus = ok:(11-15)

11. saveMessChat(m_id, chat_id, stream_id): збереження подомлення в таблиці chat на каналі
12. saveMess(m_id, chat_id, us_id, text, time): збереження повідомлення в таблиці message
13. return(message_list): отримання оновленої історії
14. chatUpdate(message_dict): оновлення історії з всіма атрибутами
15. displayingNewChat(): відображення оновленого чату

![alt text](UC-1.png)

## US-2: відправка відповіді користувачем в чаті на бажане повідомленн

учасники:

- user
- charUI
- chatService
- message
- chat

кроки:

loop(1-2)

1. selectMessage(m2_id) вибір повідомлення адресата
2. changeMessType(m2_id) зміна типу власного повідомлення з додаванням нового атрибуту - id повідомлення на яке відповідають
3. enterText(text): написання повідомлення
4. sendReq(): натискання кнопки надіслати
5. postMes(status, text, us_id, stream_id, chat_id, m2_id): запит на сервіс для обробки запиту надсилання повідомлення
6. checkMessages(us_id, m2_id): запит на отримання id останнього повідомлення користувача
7. return (lastMessId, type_m2): повернення id останнього повідомлення користувача сервісу
8. takeLastMessParam(us_id, lastMessId) запит на отримання часу коли останнє повідомлення було записано
9. return(lastTime) отримання цього часу сервісом
10. audit(status, text, us_id, lastTime, type_m2): перевірка на відповідність всім вимогам для надсилання повідомлення

ALT
auditstatus = err: (11-12)

11. return(audit_status): повернення статусу перевірки
12. postErrType(Err) відобарженя помилки із збереженим текстом та часом що залишилось почекати

auditstatus = ok:(13-17)

13. saveMessChat(m_id, chat_id, stream_id): збереження подомлення в таблиці chat на каналі
14. saveMess(m_id, chat_id, us_id, text, time, m2_id): збереження повідомлення в таблиці message
15. return(message_list): отримання оновленої історії
16. chatUpdate(message_dict): оновлення історії з всіма атрибутами
17. displayingNewChat(): відображення оновленого чату

![alt text](UC-2.png)

UC-3: видалення повідомлення користувачем з відповідним правом на трансляції (streamer, vip)

учасники:

- stremer/vip
- charUI
- chatService
- message
- chat

кроки:

loop: (1-3)

1. selectMessage(m2_id, us_status): виділення повідомлення
2. checkOrder(us_status): перевірка дозволів на взаємодії з повідомленнями
3. showAction() відобразити можливі дії
4. delete(us_id) вибрати дію видалення
5. deleteReq(m2_id, us_id) запит на видалення конкретного повідомлення
6. deleteMessMessage(m2_id). видалення повідомлення із таблиці Message
7. deleteMessChat(m2_id) видалення повідомлення із таблиці Chat
8. return (message_list) повернення списку повідомлень в чаті
9. chatUpdate(message_dict) оновлення історії з всіма атрибутами
10. displayingNewChat() відображення оновленого чату

![alt text](UC-3.png)
