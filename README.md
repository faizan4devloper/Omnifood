import React, { useState } from "react";
import Select from "react-select";
import "./Insights.css";

export function Insights() {
    const [localities] = useState([
        { value: "New York", label: "New York" },
        { value: "Los Angeles", label: "Los Angeles" },
        { value: "Chicago", label: "Chicago" },
        { value: "Houston", label: "Houston" },
        { value: "Phoenix", label: "Phoenix" }
    ]);
    const [selectedLocality, setSelectedLocality] = useState(null);

    const handleLocalityChange = (selectedOption) => {
        setSelectedLocality(selectedOption);
    };

    return (
        <div className="insights-container">
            <h3>Insights</h3>
            <div className="locality-section">
                <h4>Choose Your Locality</h4>
                <Select
                    className="dropdown"
                    value={selectedLocality}
                    onChange={handleLocalityChange}
                    options={localities}
                    placeholder="Select a locality"
                    isClearable
                />
                {selectedLocality && <div className="selected-message">You selected: {selectedLocality.label}</div>}
            </div>
        </div>
    );
}
