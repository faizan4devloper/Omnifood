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
