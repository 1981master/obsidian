pip install sqlalchemy mysql-connector-python

- create Database .py file
```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base

# MySQL connection (like Spring datasource)
DATABASE_URL = "mysql+mysqlconnector://root:1981@localhost:3306/ReactPractice"

# Create engine
engine = create_engine(DATABASE_URL, echo=True)  # echo=True shows SQL logs

# Create session factory
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

# Base class for models
Base = declarative_base()

```