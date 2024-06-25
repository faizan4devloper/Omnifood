.upload-container {
    background-color: rgba(0, 0, 0, 0.5);
    margin: 80px 0 0 10px;
    border-radius: 10px;
    width: 300px;
    display: flex;
    align-items: center; /* Vertically center chat-content */
}

.chat-content {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.chat-messages {
    flex: 1;
    max-height: 250px;
    padding: 10px;
    margin: 60px 20px;
    border-radius: 5px;
    overflow-y: auto;
    background-color: #f9f9f9;
    opacity: 0;
    animation: fadeIn 0.5s forwards;
}

.show {
    opacity: 1;
}

.hide {
    display: none;
}

/* Rest of the CSS remains unchanged */






export function ChatScreen() {
    const [messages, setMessages] = useState([]);
    const [userInput, setUserInput] = useState("");
    const [showMessages, setShowMessages] = useState(true);

    const handleSend = () => {
        if (userInput.trim()) {
            const newMessage = { sender: "user", text: userInput };
            setMessages([...messages, newMessage]);
            setUserInput("");
            setShowMessages(false); // Hide messages after sending user message
            // Simulate bot response
            setTimeout(() => {
                const botMessage = { sender: "bot", text: "This is a bot response." };
                setMessages(prevMessages => [...prevMessages, botMessage]);
                setShowMessages(true); // Show messages after receiving bot response
            }, 1000);
        }
    };

    return (
        <div className="upload-container">
            <div className="chat-content">
                <h3>Live Conversation</h3>
                <div className={`chat-messages ${showMessages ? 'show' : 'hide'}`}>
                    {messages.map((message, index) => (
                        <div key={index} className={`chat-message ${message.sender}`}>
                            {message.text}
                        </div>
                    ))}
                </div>
                <div className="chat-input">
                    <input
                        type="text"
                        value={userInput}
                        onChange={(e) => setUserInput(e.target.value)}
                        onKeyPress={(e) => e.key === "Enter" && handleSend()}
                        placeholder="Type a message..."
                    />
                    <button onClick={handleSend}><FontAwesomeIcon icon={faPaperPlane} /></button>
                </div>
            </div>
        </div>
    );
}
