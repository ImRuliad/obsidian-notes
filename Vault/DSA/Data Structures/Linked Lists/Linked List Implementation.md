

## <u> Building a Singly Linked List </u>
```python
class LinkedList:
	def __init__(self):
		self.head = None
	
	def is_empty(self):
		return self.head is None
	
	def append(self, data):
		new_node = Node(data)
		if self.is_empty():
			self.head = new_node
			return
		current = self.head
		while current.next:
			current = current.next
		current.next = new_node
	
	def prepend(self, data):
		new_node = Node(data)
		new_node.next = self.head
		self.head = new_node
	
	def insert_after(self, target_data, data):
		current = self.head
		while current and current.data != target_data:
			current = current.next
		if current is None:
			print(f"Node with data {target_data} not found")
			return
		new_node = Node(data)
		new_node.next = current.next
		current.next = new_node
	
	def delete(self, data):
		if self.is_empty():
			return
		if self.head.data == data:
			self.head = self.head.next
			return
		current = self.head
		while current.next and current.next.data != data:
			current = current.next
		if current.next:
			current.next = current.next.next
	
```