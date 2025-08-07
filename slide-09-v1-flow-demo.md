---

# V1 Flow
<div class="grid grid-cols-2 gap-4 text-xs">

<div style="position: relative; height: 400px; overflow: hidden;">

<!-- V1 Complete Request -->
<div class="absolute w-full transition-transform duration-700 ease-in-out" 
     style="top: 0px;">

**Single Request: Complete** <span v-show="$slidev.nav.clicks >= 1" style="color: #16a34a;">✓ 📤</span>
<div style="font-size: 10px; margin-top: -14px;">

<div class="bg-gray-100 p-3 rounded text-xs font-mono text-black" v-bind:style="$slidev.nav.clicks === 1 ? 'background-color: #dcfce7; border: 2px solid #16a34a;' : ''">
POST /v2/complete<br/>
{<br/>
&nbsp;&nbsp;"bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",<br/>
&nbsp;&nbsp;"user_id": "306066b7-e47a-405b-8726-ccec362858ac",<br/>
&nbsp;&nbsp;"conversation_id": "f47ac10b...",<br/>
&nbsp;&nbsp;"message": "Hello",<br/>
&nbsp;&nbsp;"webhook": "https://api.example.com/webhook",<br/>
&nbsp;&nbsp;"messages": [<br/>
&nbsp;&nbsp;&nbsp;&nbsp;{"bot": true, "content": ["Hi! How are you?"]}<br/>
&nbsp;&nbsp;],<br/>
&nbsp;&nbsp;"language": "en",<br/>
&nbsp;&nbsp;"platform": "Web",<br/>
&nbsp;&nbsp;"user_kv_pairs": {"age": 25}<br/>
}
</div>

</div>

</div>

</div>

<div>

<div v-click="2" v-show="$slidev.nav.clicks === 2" class="mt-2 text-center p-3 rounded text-black" style="background-color: #fef3c7; border: 2px solid #f59e0b;">
🤖 <strong>Bot processing message...</strong>
</div>

<div v-click="3" class="mt-2">

**Webhook Received**
<div class="bg-gray-100 p-3 rounded text-xs font-mono text-black">
{<br/>
&nbsp;&nbsp;"completion": ["Hi! Nice to meet you!"],<br/>
&nbsp;&nbsp;"id": "b2c3d4e5-f6a7-8901-bcde-f23456789012",<br/>
&nbsp;&nbsp;"media": null,<br/>
&nbsp;&nbsp;"media_id": null<br/>
}
</div>

</div>

<div v-click="3" class="mt-2 text-center p-3 rounded text-black" style="background-color: #dcfce7; border: 2px solid #16a34a;">
✅ <strong>Complete! Bot response generated and returned</strong> 🎯
</div>

</div>

</div>
