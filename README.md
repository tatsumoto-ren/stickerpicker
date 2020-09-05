# Maunium sticker picker
A fast and simple Matrix sticker picker widget. Tested on Element Web, Android & iOS.

## Discussion
Matrix room: [`#maunium:maunium.net`](https://matrix.to/#/#maunium:maunium.net)

## Importing packs from Telegram
1. (Optional) Set up a virtual environment.
   1. Create with `virtualenv -p python3 .`
   2. Activate with `source ./bin/activate`
2. Install dependencies with `pip install -r requirements.txt`
3. Run `python3 import.py <pack urls...>`
   * On the first run, it'll prompt you to log in to Matrix and Telegram.
     * The Matrix URL and access token are stored in `config.json` by default.
     * The Telethon session data is stored in `sticker-import.session` by default.
   * By default, the pack data will be written to `web/packs/`.
   * You can pass as many pack URLs as you want.
   * You can re-run the command with the same URLs to update packs.

If you want to list the URLs of all your saved packs, use `python3 import.py --list`.
This requires logging in with your account instead of a bot token.

## Enabling the sticker widget
1. Serve everything under `web/` using your webserver of choice. Make sure not to serve the
   top-level data, as `config.json` and the Telethon session file contain sensitive data.
2. Using `/devtools` in Element Web, edit the `m.widgets` account data event to have the following content:

   ```json
   {
       "stickerpicker": {
           "content": {
               "type": "m.stickerpicker",
               "url": "https://your.sticker.picker.url/index.html",
               "name": "Stickerpicker",
               "data": {}
           },
           "sender": "@you:picker.url",
           "state_key": "stickerpicker",
           "type": "m.widget",
           "id": "stickerpicker"
       }
   }
   ```

    If you do not yet have a `m.widgets` event, simply create it with that content.
    You can also [use the client-server API directly][1] instead of using Element Web.
3. Open the sticker picker and enjoy the fast sticker picking experience.

[1]: https://matrix.org/docs/spec/client_server/latest#put-matrix-client-r0-user-userid-account-data-type

## Preview
### Element Web
![Element Web](preview-element-web.png)

### Element Android
![Element Android](preview-element-android.png)
