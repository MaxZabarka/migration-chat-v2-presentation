You are creating a presentatin which will help my clients migrate my API from version 1 to version 2
counterintiuvitely, the api routes /v2 is actually semantically version 1, and /v2 route is actually version 3 semantially

you can find an openapi file at ./version-2-api.yaml for the new version of the api.
you can find examples of use of the new api, at /home/max/Documents/fanheat-chat/bruno/chat api v2/
you can find an sdk which uses the api at /home/max/Documents/priori-chat-sdk/
you can find a ui which uses the api through the sdk at /home/max/Documents/priori-chat-ui/

Please see an example of the original API at /home/max/Documents/fanheat-chat/api_demo.http. Here is an example request of the original API:

{
  "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",
  "prompt": null,
  "message": "Hola",
  "segment": null,
  "user_id": "306066b7-e47a-405b-8726-ccec362858ac",
  "webhook": "https://api.qkkie.com/chat/clonetwin/messages?token=ec550534-8317-4425-8ee6-fceba949fc03&conversation=chat-57-10628047-21400194",
  "image_id": null,
  "language": "es",
  "messages": [
    {
      "id": null,
      "bot": true,
      "content": [
        "Ehh la verdad mi mayor fantasía es tener sexo anal con alguien de la realeza, un rey, duque o algo asi, jajajj ya se que raro no?  "
      ]
    },
    {
      "id": null,
      "bot": true,
      "content": [
        "Que prefieres, tratarme como una reina delicada o como un juguete sexual y hacerme lo que tu quieras? "
      ]
    },
    {
      "id": null,
      "bot": true,
      "content": [
        "Escribeme si quieres hacer un juego de roles! Tengo algunas ideas 😈"
      ]
    }
  ],
  "platform": "Qkkie",
  "timezone": null,
  "fast_mode": null,
  "follow_up": null,
  "image_url": null,
  "max_delay": 60,
  "min_delay": 30,
  "offer_url": null,
  "bot_images": null,
  "user_images": null,
  "is_follow_up": null,
  "question_mode": null,
  "start_message": null,
  "user_freeform": null,
  "user_kv_pairs": {
    "age": 30
  },
  "conversation_id": "chat-57-10628047-21400194",
  "degrade_grammar": 1.0,
  "bot_display_name": null,
  "no_start_message": null,
  "user_display_name": null,
  "enable_protections": true,
  "chat_images_enabled": null,
  "user_can_send_photos": null,
  "use_hardcoded_conversation_starters": null
}

Not all features of the new api will be in the old api and vice versa. highlight which features are not avaialbe in the new api yet.

highlight that the original api is oone endpoint which is used to generate a completion, while the new api is baseed on adding messages
