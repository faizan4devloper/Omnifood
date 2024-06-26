<div className="section">
            <h4 onClick={() => handleExpand("ofstedRating")}>
              <span className="expand-icon">
                {expandedSection === "ofstedRating" ? (
                  <FontAwesomeIcon icon={faAngleRight} />
                ) : (
                  <FontAwesomeIcon icon={faAngleDown} />
                )}
              </span>
              Ofsted Rating
            </h4>
            {expandedSection === "ofstedRating" && (
              <div className="section-content">
                <textarea
                  placeholder="Enter Ofsted Rating here..."
                  rows={5}
                ></textarea>
              </div>
            )}
          </div>
