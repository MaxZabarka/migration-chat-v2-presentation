---

# V3 Flow

<style>
pre code { font-size: 9px !important; }
</style>

<div class="grid grid-cols-2 gap-4 text-xs">

<div style="position: relative; height: 400px; overflow: hidden;">

<!-- Step 1: Create Conversation -->
<div class="absolute w-full transition-transform duration-700 ease-in-out" 
     style="top: 0px;"
     v-bind:style="`transform: translateY(${$slidev.nav.clicks >= 6 ? '-180px' : '0px'})`">

**Step 1: Create Conversation** <span v-show="$slidev.nav.clicks >= 1" style="color: #16a34a;">✓ 📤</span>
<div style="font-size: 10px; margin-top: -14px;">

<div class="bg-gray-100 p-3 rounded text-xs font-mono text-black" v-bind:style="$slidev.nav.clicks === 1 ? 'background-color: #dcfce7; border: 2px solid #16a34a;' : ''">
POST /api/conversations<br/>
{<br/>
&nbsp;&nbsp;"bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",<br/>
&nbsp;&nbsp;"user_id": "306066b7-e47a-405b-8726-ccec362858ac",<br/>
&nbsp;&nbsp;"create_user_if_not_exists": true,<br/>
&nbsp;&nbsp;"webhook": "https://api.example.com/webhook"<br/>
}
</div>

</div>

</div>

<!-- Step 2: Send Message -->
<div v-click="2" class="absolute w-full transition-transform duration-700 ease-in-out" 
     style="top: 180px;"
     v-bind:style="`transform: translateY(${$slidev.nav.clicks >= 6 ? '-180px' : '0px'})`">

**Step 2: Send Message** <span v-show="$slidev.nav.clicks >= 4" style="color: #16a34a;">✓ 📤</span>
<div class="text-xs" style="margin-top: -14px;">

<div class="bg-gray-100 p-3 rounded text-xs font-mono text-black" v-bind:style="$slidev.nav.clicks === 4 ? 'background-color: #dcfce7; border: 2px solid #16a34a;' : ''">
POST /api/conversations/<span v-mark="{ at: 3, color: '#DC2626', type: 'underline' }" style="font-weight: bold; color: #DC2626;">f47ac10b...</span>/messages<br/>
{<br/>
&nbsp;&nbsp;<span style="background-color: #DBEAFE; padding: 2px 4px; border-radius: 3px;">"message": {<br/>
&nbsp;&nbsp;&nbsp;&nbsp;"text": "Hello",<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="font-weight: bold;">"from_bot": false</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;"attached_media": null<br/>
&nbsp;&nbsp;}</span><br/>
}
</div>

</div>

</div>

<!-- Step 3: Webhook Received -->
<div v-click="6" class="absolute w-full transition-transform duration-700 ease-in-out" 
     style="top: 360px;"
     v-bind:style="`transform: translateY(${$slidev.nav.clicks >= 6 ? '-180px' : '0px'})`">

**Step 3: Webhook Received**
<div class="text-xs" style="margin-top: -14px;">

<div class="bg-gray-100 p-3 rounded text-xs font-mono text-black">
{<br/>
&nbsp;&nbsp;"event": "message.created",<br/>
&nbsp;&nbsp;"conversation_id": <span style="font-weight: bold; color: #DC2626;">"f47ac10b..."</span>,<br/>
&nbsp;&nbsp;<span style="background-color: #FED7AA; padding: 2px 4px; border-radius: 3px;">"message": {<br/>
&nbsp;&nbsp;&nbsp;&nbsp;"id": "b2c3d4e5-f6a7-8901-bcde-f23456789012",<br/>
&nbsp;&nbsp;&nbsp;&nbsp;"text": "Hi! How are you?",<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="font-weight: bold;">"from_bot": true</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;"sent_at": 1640995205,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;"message_tone": "Friendly"<br/>
&nbsp;&nbsp;}</span><br/>
}
</div>

</div>

</div>

</div>

<div>

<div v-click="1" class="mt-2">

**Conversation State**
<div class="bg-gray-100 p-3 rounded text-xs font-mono text-black">
{<br/>
&nbsp;&nbsp;"id": <span v-mark="{ at: 3, color: '#DC2626', type: 'underline' }" style="font-weight: bold; color: #DC2626;">"f47ac10b..."</span>,<br/>
&nbsp;&nbsp;"bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",<br/>
&nbsp;&nbsp;"user_id": "306066b7-e47a-405b-8726-ccec362858ac",<br/>
&nbsp;&nbsp;"webhook": "https://api.example.com/webhook",<br/>
&nbsp;&nbsp;"messages": [<span v-click="4" style="opacity: 0; position: absolute;" v-bind:style="$slidev.nav.clicks >= 4 ? 'position: static; opacity: 1;' : ''"><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="background-color: #DBEAFE; padding: 2px 4px; border-radius: 3px;">{<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"text": "Hello",<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="font-weight: bold;">"from_bot": false</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sent_at": 1640995200<br/>
&nbsp;&nbsp;&nbsp;&nbsp;}</span></span><span v-click="6" style="opacity: 0; position: absolute;" v-bind:style="$slidev.nav.clicks >= 6 ? 'position: static; opacity: 1;' : ''">,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="background-color: #FED7AA; padding: 2px 4px; border-radius: 3px;">{<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "b2c3d4e5-f6a7-8901-bcde-f23456789012",<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"text": "Hi! How are you?",<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="font-weight: bold;">"from_bot": true</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sent_at": 1640995205,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"message_tone": "Friendly"<br/>
&nbsp;&nbsp;&nbsp;&nbsp;}</span></span><br/>
&nbsp;&nbsp;]<br/>
}
</div>

</div>

<div v-click="5" class="mt-2 text-center p-3 rounded text-black" v-bind:style="$slidev.nav.clicks === 6 ? 'background-color: #dcfce7; border: 2px solid #16a34a;' : 'background-color: #fef3c7; border: 2px solid #f59e0b;'">
<span v-show="$slidev.nav.clicks === 5">🤖 <strong>New user message detected, bot generating...</strong></span>
<span v-show="$slidev.nav.clicks >= 6">✅ <strong>AI msg generated! Sent webhook, added message to history</strong> 📤</span>
</div>


</div>

</div>