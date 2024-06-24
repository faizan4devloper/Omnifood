import React, { useState } from "react";
import "./Insights.css";

export function Insights() {
    const [localities] = useState(["New York", "Los Angeles", "Chicago", "Houston", "Phoenix"]);
    const [selectedLocality, setSelectedLocality] = useState("");

    const handleLocalityClick = (locality) => {
        setSelectedLocality(locality);
    };

    return (
        <div className="insights-container">
            <h3>Insights</h3>
            <div className="locality-section">
                <h4>Choose Your Locality</h4>
                <div className="localities">
                    {localities.map((locality, index) => (
                        <div
                            key={index}
                            className={`locality ${selectedLocality === locality ? 'selected' : ''}`}
                            onClick={() => handleLocalityClick(locality)}
                        >
                            {locality}
                        </div>
                    ))}
                </div>
                {selectedLocality && <div className="selected-message">You selected: {selectedLocality}</div>}
            </div>
        </div>
    );
}









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
}

.locality-section h4 {
    color: #fff;
    margin-bottom: 10px;
}

.localities {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.locality {
    background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
    color: white;
    padding: 10px 20px;
    margin: 5px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.locality:hover {
    background: linear-gradient(90deg, #1f77f6 0%, #6f36cd 100%);
    transform: scale(1.05);
}

.locality.selected {
    background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
    border: 2px solid #fff;
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
