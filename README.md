## Challenge
This project involves performing the main operations between vectors and matrices.

```python
class Matrix:
    def __init__(self,lists) ->  list:
        self.lists=lists
    def __repr__(self):
        return f"{self.lists}"
    def is_squared(self) -> bool:
        return self.size()[0]==self.size()[1]
    def pretty_print(self):
        for i in self.lists:
            print("|", end="") 
            for j in i:
                print(j, end=" ")
            print("|")     
    def get_element(self,row,column) -> float:
        return self.lists[row-1][column-1]
    def size(self) -> tuple:
        return (len(self.lists),len(self.lists[0]))
    def add(self, new_matrix: 'Matrix'):
        self.new_matrix=new_matrix
        if self.size()==new_matrix.size():
            result=[[0 for _ in range(len(self.lists[0]))] for _ in range(len(self.lists))]
            for i in range(len(self.lists)):
                for j in range(len(self.lists[0])):
                    result[i][j]=self.get_element(i+1,j+1)+ new_matrix.get_element(i+1,j+1)
            return Matrix(result)
        else:return []
        
    def multiply(self, new_matrix: 'Matrix'):
        self.new_matrix=new_matrix
        if self.size()[1]==new_matrix.size()[0]:
            result=[[0 for _ in range(new_matrix.size()[1])] for _ in range(self.size()[0])]
            for i in range(self.size()[0]):
                for j in range(new_matrix.size()[1]):
                    result[i][j]=sum(self.get_element(i+1,k+1)*new_matrix.get_element(k+1,j+1) for k in range(self.size()[1]))
            return Matrix(result)
        else:return []

class Vector(Matrix):
    def __init__(self,lists):
        super().__init__(lists)
    def is_column(self) ->bool:
        if self.size()[1] == 1:return True
        else:return False
    def is_row(self) ->bool:
        if self.size()[0] == 1: return True
        else: return False
    def norm(self):
        return (self.multiply(self))**(1/2)
    def multiply(self, new_vector:'Vector'):
        if self.is_row() and new_vector.is_column():
            return sum(self.get_element(i+1,1)*new_vector.get_element(1,i+1) for i in range(self.size()[0]))
        elif self.is_column() and new_vector.is_row():
            return sum(self.get_element(1,i+1)*new_vector.get_element(i+1,1) for i in range(new_vector.size()[0]))
        elif self.is_column() and new_vector.is_column():
            return sum(self.get_element(i+1,1)*new_vector.get_element(i+1,1) for i in range(self.size()[0]))
        elif self.is_row() and new_vector.is_row():
            return sum(self.get_element(1,i+1)*new_vector.get_element(1,i+1) for i in range(self.size()[0]))
        else: return []
```
