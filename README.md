# pytest-api-sql-test-framework
“Automated Test Framework: Built PyTest-based testing framework with SQL validation utilities…”
## Automated API Test Framework

This project demonstrates how to build automated API tests using PyTest
with direct SQL validation.

### Why this matters
In many systems, API responses may succeed while database state is incorrect.
These tests validate both layers to catch hidden bugs.

### What is tested
- API response correctness
- Database state consistency
- Regression behavior across endpoints

### Tools
- Flask
- PyTest
- SQLite


def test_create_user(client, db_session):
    response = client.post("/users", json={
        "name": "Alice",
        "email": "alice@test.com"
    })

    assert response.status_code == 200

    user = db_session.execute(
        "SELECT * FROM users WHERE email='alice@test.com'"
    ).fetchone()

    assert user is not None
