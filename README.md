import React, { useEffect, useState } from "react";
import axios from "axios";

const UserList = () => {
  const [listOfUser, setListOfUser] = useState([]);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/users")
      .then((response) => {
        setListOfUser(response.data);
      })
      .catch((error) => {
        console.error("Error fetching data:", error);
      });
  }, []);

  return (
    <div style={{ padding: "20px", fontFamily: "Arial, sans-serif" }}>
      <h2 style={{ textAlign: "center", marginBottom: "20px", color: "#333" }}>
        User List
      </h2>
      <div
        style={{
          display: "grid",
          gridTemplateColumns: "repeat(auto-fit, minmax(250px, 1fr))",
          gap: "20px",
        }}
      >
        {listOfUser.map((user) => (
          <div
            key={user.id}
            style={{
              padding: "20px",
              border: "1px solid #ddd",
              borderRadius: "12px",
              backgroundColor: "#fff",
              boxShadow: "0 4px 6px rgba(0,0,0,0.1)",
              transition: "transform 0.2s",
            }}
            onMouseEnter={(e) => (e.currentTarget.style.transform = "scale(1.03)")}
            onMouseLeave={(e) => (e.currentTarget.style.transform = "scale(1)")}
          >
            <h3 style={{ marginBottom: "10px", color: "#0077cc" }}>
              {user.name}
            </h3>
            <p>
              <strong>Email:</strong> {user.email}
            </p>
            <p>
              <strong>Phone:</strong> {user.phone}
            </p>
            <p>
              <strong>Company:</strong> {user.company.name}
            </p>
            <p>
              <strong>Website:</strong>{" "}
              <a href={`http://${user.website}`} target="_blank" rel="noreferrer">
                {user.website}
              </a>
            </p>
          </div>
        ))}
      </div>
    </div>
  );
};

export default UserList;
