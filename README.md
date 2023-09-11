# code-share
import React, { useState, useEffect } from 'react';
import 'bootstrap/dist/css/bootstrap.min.css';

const App = () => {
  const [rewardItems, setRewardItems] = useState([]);
  const [personas, setPersonas] = useState([]);
  const [filters, setFilters] = useState({
    showNonAvailable: false,
    showAvailable: false,
    showSaleItems: false,
    showEnoughPoints: false,
  });

  useEffect(() => {
    // Fetch reward items from API
    // Replace with actual API endpoint
    fetch('/api/rewardItems')
      .then((response) => response.json())
      .then((data) => setRewardItems(data));

    // Fetch personas from API
    // Replace with actual API endpoint
    fetch('/api/personas')
      .then((response) => response.json())
      .then((data) => setPersonas(data));
  }, []);

  const applyFilters = () => {
    // Apply filters to reward items
    let filteredItems = rewardItems;

    if (!filters.showNonAvailable) {
      filteredItems = filteredItems.filter((item) => item.status === 'active');
    }

    if (filters.showAvailable) {
      filteredItems = filteredItems.filter((item) => item.status === 'active');
    }

    if (filters.showSaleItems) {
      filteredItems = filteredItems.filter((item) => item.isOnSale);
    }

    if (filters.showEnoughPoints) {
      // Replace with logic to filter items based on persona points
      // For example, check if the persona has enough points for each item
      filteredItems = filteredItems.filter((item) => item.points <= personaPoints);
    }

    return filteredItems;
  };

  const personaPoints = 1000; // Replace with the actual points for the persona

  const filteredRewardItems = applyFilters();

  const clearFilters = () => {
    setFilters({
      showNonAvailable: false,
      showAvailable: false,
      showSaleItems: false,
      showEnoughPoints: false,
    });
  };

  return (
    <div className="container mt-5">
      <h1>Reward Items</h1>

      <div className="mb-3">
        <button className="btn btn-primary mr-2" onClick={() => setFilters({ ...filters, showNonAvailable: !filters.showNonAvailable })}>
          Show Non-Available Items
        </button>
        <button className="btn btn-primary mr-2" onClick={() => setFilters({ ...filters, showAvailable: !filters.showAvailable })}>
          Show Available Items
        </button>
        <button className="btn btn-primary mr-2" onClick={() => setFilters({ ...filters, showSaleItems: !filters.showSaleItems })}>
          Show Sale Items
        </button>
        <button className="btn btn-primary" onClick={() => setFilters({ ...filters, showEnoughPoints: !filters.showEnoughPoints })}>
          Show Items You Have Enough Points For
        </button>
        <button className="btn btn-danger ml-2" onClick={clearFilters}>
          Clear Filters
        </button>
      </div>

      <table className="table">
        <thead>
          <tr>
            <th>Name</th>
            <th>Status</th>
            <th>Points</th>
            <th>Sale</th>
          </tr>
        </thead>
        <tbody>
          {filteredRewardItems.map((item) => (
            <tr key={item.id}>
              <td>{item.name}</td>
              <td>{item.status}</td>
              <td>{item.points}</td>
              <td>{item.isOnSale ? 'Yes' : 'No'}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default App;
