npm create vite@latest . --template react

npm install

npm install -D tailwindcss postcss autoprefixer gh-pages
npx tailwindcss init -p

content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"]

@tailwind base;
@tailwind components;
@tailwind utilities;

import React from "react";

const messagesInit = [
  { sender: "bot", text: "Здравствуйте! Чем могу помочь по вопросам ЖКХ?" },
];

function App() {
  const [chat, setChat] = React.useState(messagesInit);
  const [input, setInput] = React.useState("");

  const sendMessage = () => {
    if (!input.trim()) return;
    const userMessage = { sender: "user", text: input };
    const botMessage = {
      sender: "bot",
      text: "Спасибо за ваш запрос. Мы свяжемся с вами в ближайшее время!",
    };
    setChat([...chat, userMessage, botMessage]);
    setInput("");
  };

  return (
    <div className="min-h-screen bg-gray-100 p-4 flex flex-col items-center">
      <h1 className="text-3xl font-bold mb-4">ЖКХ Чат-Бот</h1>
      <div className="bg-white shadow rounded p-4 w-full max-w-xl h-96 overflow-y-auto">
        {chat.map((msg, idx) => (
          <div
            key={idx}
            className={`my-2 p-2 rounded-lg max-w-xs ${
              msg.sender === "bot" ? "bg-blue-100 text-left" : "bg-green-100 ml-auto text-right"
            }`}
          >
            {msg.text}
          </div>
        ))}
      </div>
      <div className="flex gap-2 mt-4 w-full max-w-xl">
        <input
          className="flex-1 p-2 border rounded"
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="Введите сообщение..."
        />
        <button
          className="bg-blue-500 text-white px-4 rounded"
          onClick={sendMessage}
        >
          Отправить
        </button>
      </div>
    </div>
  );
}

export default App;

"homepage": "https://shimiyatsu.github.io/yekhiori",

"scripts": {
  "dev": "vite",
  "build": "vite build",
  "preview": "vite preview",
  "predeploy": "npm run build",
  "deploy": "gh-pages -d dist"
}

git add .
git commit -m "initial chatbot setup"
git branch -M main
git remote add origin https://github.com/shimiyatsu/yekhiori.git
git push -u origin main
npm run deploy

