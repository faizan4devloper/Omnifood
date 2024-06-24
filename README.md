.insights-container {
    background-color: rgba(0, 0, 0, 0.5);
    margin: 80px 0 0 10px;
    border-radius: 10px;
    width: 400px;
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    transition: transform 0.3s ease-in-out;
}

.insights-container:hover {
    transform: scale(1.02);
}

.insights-container h3 {
    text-align: center;
    color: #fff;
}

.locality-section {
    margin-top: 20px;
    text-align: center;
    background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    animation: fadeIn 0.5s ease-in-out;
}

.locality-section h4 {
    color: #fff;
    margin-bottom: 20px;
    font-size: 1.5em;
    text-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
}

.locality-dropdown {
    width: 80%;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
    font-size: 1em;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
    background: #fff;
    color: #333;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.locality-dropdown:hover {
    background-color: #f1f1f1;
    transform: scale(1.05);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
}

.selected-message {
    margin-top: 15px;
    color: #fff;
    font-size: 1.2em;
    animation: fadeIn 0.5s ease-in-out;
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}
