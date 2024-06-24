import React, { useState } from "react";
import "./Insights.css";

export function Insights() {
    const [localities] = useState(["New York", "Los Angeles", "Chicago", "Houston", "Phoenix"]);
    const [filteredLocalities, setFilteredLocalities] = useState(localities);
    const [selectedLocality, setSelectedLocality] = useState("");
    const [showDropdown, setShowDropdown] = useState(false);
    const [searchTerm, setSearchTerm] = useState("");

    const handleLocalityClick = (locality) => {
        setSelectedLocality(locality);
        setShowDropdown(false);
    };

    const handleSearchChange = (e) => {
        setSearchTerm(e.target.value);
        const filtered = localities.filter(locality =>
            locality.toLowerCase().includes(e.target.value.toLowerCase())
        );
        setFilteredLocalities(filtered);
    };

    const toggleDropdown = () => {
        setShowDropdown(!showDropdown);
    };

    return (
        <div className="insights-container">
            <h3>Insights</h3>
            <div className="locality-section">
                <h4>Choose Your Locality</h4>
                <div className="dropdown">
                    <button className="dropdown-button" onClick={toggleDropdown}>
                        {selectedLocality ? selectedLocality : "Select a locality"}
                    </button>
                    {showDropdown && (
                        <div className="dropdown-content">
                            <input
                                type="text"
                                placeholder="Search localities..."
                                value={searchTerm}
                                onChange={handleSearchChange}
                                className="dropdown-search"
                            />
                            <ul>
                                {filteredLocalities.map((locality, index) => (
                                    <li
                                        key={index}
                                        className="dropdown-item"
                                        onClick={() => handleLocalityClick(locality)}
                                    >
                                        {locality}
                                    </li>
                                ))}
                            </ul>
                        </div>
                    )}
                </div>
                {selectedLocality && <div className="selected-message">You selected: {selectedLocality}</div>}
            </div>
        </div>
    );
}
