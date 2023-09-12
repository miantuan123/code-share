# code-share
import React, { useState } from 'react';
import Form from 'react-bootstrap/Form';

function RewardFilter({ onFilterChange }) {
  const [filterOptions, setFilterOptions] = useState({
    active: false,
    inactive: false,
    sale: false,
  });

  const handleFilterChange = (event) => {
    const { name, checked } = event.target;
    setFilterOptions({ ...filterOptions, [name]: checked });
    onFilterChange({ ...filterOptions, [name]: checked });
  };

  return (
    <Form>
      <Form.Check
        type="checkbox"
        label="Active"
        name="active"
        checked={filterOptions.active}
        onChange={handleFilterChange}
      />
      <Form.Check
        type="checkbox"
        label="Inactive"
        name="inactive"
        checked={filterOptions.inactive}
        onChange={handleFilterChange}
      />
      <Form.Check
        type="checkbox"
        label="Sale"
        name="sale"
        checked={filterOptions.sale}
        onChange={handleFilterChange}
      />
    </Form>
  );
}

export default RewardFilter;
