# LinkedLists are basically video games
Yeah you read that right,  they are basically the same thing, except one takes litteraly years to be done and cost like millions of dolars, and the other one you can just buy on steam, test it for like, two hours and get you money back... 

Okay okay, back to the important stuff. 

When you start a new game, usually they all follow the same idea, you have your first mission, and when you finish this mission, the next mission gets unlocked and you get to see where you need to go to start it, and some games  even let you check how many missions are avaiable, and how much progress you have done.

LinkedLists works the same whey, but insted of missions, you have Nodes and insted of how many missions, you have how many nodes there are.

So basically:
 - Game == LinkedList 
 - Mission == Node

## Keep talking, Keep talking...

A game’s mission, have basically two informations, the mission itself, and where you need to go to start the next mission, you can’t skip all missions and go straight to the last one, because the first mission only unlocks the very next one, and then the next one. So, to get to the last mission, you need to through the hole game.

That’s exactly how linkedLists works, you have, the very first node, and how many node in the list, that’s it, if you want to get to the last node, you have to go through the hole list, one by one, so we can think of linkedLists and nodes, like this:

Game

-   First mission
-   How many missions

LinkedList

-   First node
-   How many nodes

Game Mission

-   What you need to do
-   Where is the next mission

List Node

-   The stored data
-   Where is the next node


## But what is this Node thing ??
Nodes are super simple, they are basically this:

    public static class Node<T> {
    
        T data; 			//(The stored data)
        Node<T> next; 		//(Where is the next node)
        
		public Node(T data) {
	            this.data = data;
	            this.next = null;
	        }
    }

// insert image later;

And the LinkedList is also simple, they look like this:

    public class MyLinkedList<T> {
	    private Node<T> head; 		//(First node)
	    private int length = 0; 	//(How many nodes)
    }
// insert image later;

## Wait, that's it ??
Of course not, there are no methods, this is not magic, we are just getting started :)

Basically the main thing that a LinkedList does, is to **Link** a bunch of nodes together, creating a **List** 
(i wonder where did the name came from...), now let's see how the LinkedList do this.

When we insert a new node to our list, we can insert it, at the end, at the the begin or anywhere in the list, so we need methods for all this operations, but let's say we want to insert a node at the begin of our list, and it's our very first node, so there are a couple things we need to do:

 1. Create a Node, and store the data that we want;
 2. Set where is our next node, since we are inserting it at the begin, the next one, will be the "head" field of our list;
 3. Set the list "head" field,  to be our new first node;
 4. Increase the Length of our List by one;

Now let's do this:

    public void insertAtBegin(T data) {
        Node<T> newNode = new Node<>(data);		//1. Create a Node, and store the data that we want;
        newNode.next = head; 					//2. Set where is our next node;
        head = newNode; 						//3. Set the list "head" field, to be our new first node;
        length++; 								//4. Increase the Length of our List by one;
    }

//insert image

If we think about this in game terms, it's like wee just created our first mission.

Now think about this method, if we decide to add a second node at the begin of the list, it will create a new node, point it's next field to the node we already had, and point the list head, to this newNode we just created.

// insert image or gif

And we can do this, how many times we want, with as many nodes we need 
(actually, until our PC runs out of memory and crashes)

Now let's say we want to add a new mission to our game, but this time, it's a mission at the end of the game, so what we need to do, is to point the last mission, to our new mission. But remember, the player needs to go through the hole game, he can't skip any mission, now let's talk in boring therms, we need to start at the head of the list, iterate through the list, until we find a node, that it's head is pointing to null, which means that we are at the last node, so now we point it's head to our new node, and increase the length of our list :)

Just like this:

    public void insertAtEnd(T data) {
        Node<T> newNode = new Node<>(data);
        if (head == null) { 					// If the head of the list is null, then this node, is the first one being inserted;
            head = newNode;
        } else {
            Node<T> current = head; 			// It creates a copy of the head, so it can iterate through the list, but preserve the actual head of the list;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode; 			// As soon as it finds a node where the "next" field is null, it means that we are at the end of the list, so we can set it as the newNode being added;
        }
        length++;
    }

super cool right ? but what if our first mission is super boring, and we need to replace it ? it's going to be completely diferente, but at the and of it, i will point to the same starting point of the second mission, that we already had. We need to break the problem in two steps, first we need to remove the old one from the begin of the list, then insert the new one, we already know how to insertAtBegin, now let's se how to:

 removeFromBegin:
 1. Store the current "head" of the list;
 2. Checks if it's null, because if it's, there is nothing to be removed
 3. Update the head of the list, to be the current "head.next" node;
 4. Set the previus first node "head" field to be null;
 5. Decrease the length of the list by one;

Now for real:

    public void removeFromBegin() {
        Node<T> node = head;		//(1. Store the current "head" of the list;)
        if (node != null) {			//(2. Checks if it's null, because if it's, there is nothing to be removed)
            head = node.next;		//(3. Update the head of the list, to be the current "head.next" node;)
            node.next = null;		//(4. Set the previus first node "head" field to be null;)
            length--;				//(5. Decrease the length of the list by one;)
        }
    }
