from flask import Flask, request, send_file
from gtts import gTTS
import os

app = Flask(__name__)

@app.route('/')
def index():
    return '''
    <form method="post" action="/convert">
        <textarea name="text" rows="4" cols="50"></textarea>
        <input type="submit" value="Convert to Speech">
    </form>
    '''

@app.route('/convert', methods=['POST'])
def convert_to_speech():
    text = request.form['text']
    tts = gTTS(text=text, lang='ko')
    tts.save("output.mp3")
    return send_file("output.mp3", as_attachment=True)



if __name__ == '__main__':
    app.run(debug=True)

