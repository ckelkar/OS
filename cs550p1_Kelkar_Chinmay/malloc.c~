#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<inttypes.h>
#include<sys/types.h>



struct node;

typedef struct node_link  //stores left,right and parent address.
{
struct node *left,*right, *parent;
}node_link;

typedef struct node // stores size and node_link array. node_link[0] corresponds to size links node_link[1] corresponds to address links
{
size_t size;
struct node_link links[2];
}block_t;

block_t sentinal_node = {0,{{NULL, NULL, NULL}, {NULL, NULL, NULL}}}; //Initialize sentinal node
block_t *root,*sizeroot,*addressroot=NULL;
//void *C550_malloc(size_t);

block_t *search_bst(size_t sz) //function which searches for the best fit size
{
sz=sz-sizeof(size_t);
block_t *temp;
	if(sentinal_node.links[0].left==NULL)
	{
	//printf("\ntree is empty.");
	temp=NULL;
	}
	else
	{
	//printf("\nIthe alo");
	temp=sentinal_node.links[0].left;
		if(sz<= temp->size && temp->links[0].left==NULL && temp->links[0].right==NULL)
		{
		return temp;
		}
		else
		{
		while(1)
		{
		       
			
			if(temp->size > sz && temp->links[0].left!=NULL) //if size is less than root search in left subtree
			{
			//printf("\ntemp=%lu",temp);
			temp=temp->links[0].left;
			
			//printf("\nwent to left");
			//printf("\nafter going to left address is=%lu",temp);
			//printf("now at address:%lu",(uintptr_t)temp);
			}
			else if(temp->size < sz && temp->links[0].right!=NULL) //if size is greater than root then traverse right subtree
			{
			temp=temp->links[0].right;
			//printf("\nwent to right");
			//printf("now at address:%lu",(uintptr_t)temp);
			}
			else if(temp->size == sz)
			{
			//printf("\ncame out");
			break;
			}
			else 
			{
			break;
			}
		}			
		
			if(sz<=temp->size)
			{
			//printf("\nsz<=temp size");
			return temp;
			}
			
			else
			{

				while(sz > temp->size) //until size is greater than size node, traverse parent
				{
					//printf("inside while");
					if(temp->links[0].parent==NULL)
					{
					//printf("\ntemp=%lu",temp);
					//printf("\nnot found =%lu",temp->links[0].parent);
					temp=NULL;
					break;
					}
					else
					{
					//printf("\ntraversed to parent");
					temp=temp->links[0].parent;
					}
				}
			}
		}
	}
return temp;
}

void deletesize(block_t *found) //function which deletes node in size BST
{
	if(found->links[0].left==NULL && found->links[0].right==NULL)		//Node to be removed has no children.
	{
		//printf("\nhere");
		if(found->links[0].parent!=NULL)
		{
			if(found->links[0].parent->size > found->size) 
			{
			found->links[0].parent->links[0].left=NULL;
			}
			else
			{
			found->links[0].parent->links[0].right=NULL;
			}
		
		}
		else
		{
		sentinal_node.links[0].left= NULL;
		sentinal_node.links[0].right=NULL;
		}
	found->links[0].parent=NULL;
	
	}

	else if(found->links[0].left==NULL || found->links[0].right==NULL) //Node to be removed has one child.
	{
		//printf("\nhere");
		if(found->links[0].left==NULL && found->links[0].parent==NULL)
		{
		sentinal_node.links[0].right=found->links[0].right;
		sentinal_node.links[0].left=sentinal_node.links[0].right;
		found->links[0].right->links[0].parent=NULL;
		}
		else if(found->links[0].right==NULL && found->links[0].parent==NULL)
		{
		sentinal_node.links[0].left=found->links[0].left;
		sentinal_node.links[0].right=found->links[0].left;
		found->links[0].left->links[0].parent=NULL;
		}
		else
		{
			if(found->links[0].parent->size > found->size)
			{
			//printf("\nhere");
			found->links[0].parent->links[0].left=found->links[0].left;
			found->links[0].left->links[0].parent=found->links[0].parent;
			}
			else
			{
			//printf("\nhere");
			found->links[0].parent->links[0].right=found->links[0].right;
			found->links[0].right->links[0].parent=found->links[0].parent;
			}
		}
	found->links[0].left=NULL;
	found->links[0].right=NULL;
	}
	
	else                          //Node to be removed has two children
	{
	block_t *temp=found;
	
	temp=temp->links[0].left;
	
	
		while(temp->links[0].right!=NULL) 
		{
			if(temp->links[0].left==NULL && temp->links[0].right==NULL)
			{
			break;
			}
			else
			{
			temp=temp->links[0].right;
			}
		}
		if(found->links[0].parent==NULL)
		{

			if(temp->links[0].parent==found)
			{
			temp->links[0].right=found->links[0].right;
			found->links[0].right->links[0].parent=temp;
			}
			else
			{
			temp->links[0].right=found->links[0].right;
			temp->links[0].left=found->links[0].left;
			temp->links[0].parent->links[0].right=NULL;
			found->links[0].left->links[0].parent=temp;
			found->links[0].right->links[0].parent=temp;
			
			}
		found->links[0].left=NULL;
		found->links[0].right=NULL;
		found->links[0].parent=NULL;
		temp->links[0].parent=NULL;
		sentinal_node.links[0].right=temp;
		sentinal_node.links[0].left=temp;
		}	

		else
		{
			
			if(temp->links[0].parent==found)
			{
			temp->links[0].right=found->links[0].right;
			found->links[0].right->links[0].parent=temp;
				if(found->links[0].parent->size <= found->size)
				{
				found->links[0].parent->links[0].right=temp;
				}
				else
				{
				found->links[0].parent->links[0].left=temp;
				}
			}
			
			else
			{
			//printf("\nhere");
			temp->links[0].right=found->links[0].right;
			temp->links[0].left=found->links[0].left;
			temp->links[0].parent->links[0].right=NULL;
				if(found->links[0].parent->size <= found->size)
				{
				found->links[0].parent->links[0].right=temp;
				}
				else
				{
				found->links[0].parent->links[0].left=temp;
				}
			}	
		//printf("\nhere");
		temp->links[0].parent=found->links[0].parent;
		found->links[0].left=NULL;
		found->links[0].right=NULL;
		found->links[0].parent=NULL;	
		}
	}	
}
	


void deleteaddress(block_t *found) //function which deletes node in address BST
{
//printf("\nin delete by address function");
if(found->links[1].left==NULL && found->links[1].right==NULL)		//Node to be removed has no children(sizewise).
	{
		
		if(found->links[1].parent!=NULL)
		{
			if(found->links[1].parent > found)
			{
			found->links[1].parent->links[1].left=NULL;
			}
			else
			{
			found->links[1].parent->links[1].right=NULL;
			}
		
		}
		else
		{
		sentinal_node.links[1].left= NULL;
		sentinal_node.links[1].right=NULL;
		}
	found->links[1].parent=NULL;
	
	}

	else if(found->links[1].left==NULL || found->links[1].right==NULL)   //Node to be removed has one child
	{
	
		
		if(found->links[1].left==NULL && found->links[1].parent==NULL)
		{
		sentinal_node.links[1].right=found->links[1].right;
		sentinal_node.links[1].left=found->links[1].right;
		found->links[1].right->links[1].parent=NULL;
		addressroot=sentinal_node.links[1].right;
		}
		else if(found->links[1].right==NULL && found->links[1].parent==NULL)
		{
		sentinal_node.links[1].left=found->links[1].left;
		sentinal_node.links[1].right=found->links[1].left;
		found->links[1].left->links[1].parent=NULL;
		addressroot=sentinal_node.links[1].left;
		}
		else
		{
		
			if(found->links[1].parent > found)
			{
			//printf("\nhere");
			found->links[1].parent->links[1].left=found->links[1].left;
			found->links[1].left->links[1].parent=found->links[1].parent;
			}
			else
			{
			
			found->links[1].parent->links[1].right=found->links[1].right;
			found->links[1].right->links[1].parent=found->links[1].parent;
			}
		}
	found->links[1].left=NULL;
	found->links[1].right=NULL;
	}
	
	else					//Node to be removed has two children
	{
	block_t *temp=found;
	
	temp=temp->links[1].left;
	
	
		while(temp->links[1].right!=NULL) 
		{
			if(temp->links[1].left==NULL && temp->links[1].right==NULL)
			{
			break;
			}
			else
			{
			temp=temp->links[1].right;
			}
		}
		if(found->links[1].parent==NULL)
		{

			if(temp->links[1].parent==found)
			{
			temp->links[1].right=found->links[1].right;
			found->links[1].right->links[1].parent=temp;
			}
			else
			{
			temp->links[1].right=found->links[1].right;
			temp->links[1].left=found->links[1].left;
			temp->links[1].parent->links[1].right=NULL;
			found->links[1].left->links[1].parent=temp;
			found->links[1].right->links[1].parent=temp;
			
			}
		found->links[1].left=NULL;
		found->links[1].right=NULL;
		found->links[1].parent=NULL;
		temp->links[1].parent=NULL;
		sentinal_node.links[1].right=temp;
		sentinal_node.links[1].left=temp;
		}	

		else
		{
			
			if(temp->links[1].parent==found)
			{
			temp->links[1].right=found->links[1].right;
			found->links[1].right->links[1].parent=temp;
				if(found->links[1].parent<= found)
				{
				found->links[1].parent->links[1].right=temp;
				}
				else
				{
				found->links[1].parent->links[1].left=temp;
				}
			}
			
			else
			{
			temp->links[1].right=found->links[1].right;
			temp->links[1].left=found->links[1].left;
			temp->links[1].parent->links[1].right=NULL;
				if(found->links[1].parent <= found)
				{
				found->links[1].parent->links[1].right=temp;
				}
				else
				{
				found->links[1].parent->links[1].left=temp;
				}
			}	
		temp->links[1].parent=found->links[1].parent;
		found->links[1].left=NULL;
		found->links[1].right=NULL;
		found->links[1].parent=NULL;	
		}
	}	
}

void insert_BST_size(block_t *root,block_t *bp)  //Inserts node in size BST
{
	//printf("\nsize of the root=%lu",(uintptr_t)root->size);
	//printf("\nee of the node to be inserted=%lu",bp->size);
	struct node *temp;
	if(root==NULL)
	{
	
 	sentinal_node.links[0].right=bp;
	sentinal_node.links[0].left=bp;
	bp->links[0].parent=NULL;
	bp->links[0].left=NULL;
	bp->links[0].right=NULL;
	//printf("\nRoot created");
	}
	else
	{
	
	//printf("\nin else part");
	temp=root;
		while(1)
		{
		
			if(temp->size>bp->size && temp->links[0].left==NULL)
			{
			temp->links[0].left=bp;
			bp->links[0].parent=temp;
			bp->links[0].left=NULL;
			bp->links[0].right=NULL;
			break;
			}
			else if(temp->size>bp->size && temp->links[0].left!=NULL)
			{
			temp=temp->links[0].left;
			}
			else if(temp->size<=bp->size && temp->links[0].right==NULL)
			{
			temp->links[0].right=bp;
			bp->links[0].parent=temp;
			bp->links[0].left=NULL;
			bp->links[0].right=NULL;
			break;
			}
			else
			{
			//printf("\n%lu",temp->links[0].right);
			temp=temp->links[0].right;
			//printf("\n%lu",temp->size);
			}
		}
	}
	
}

void insert_BST_address(block_t *root,block_t *bp)	//Inserts node in address BST
{
	struct node *temp;
	if(root==NULL)
	{

	sentinal_node.links[1].left=bp;
	sentinal_node.links[1].right=bp;
	bp->links[1].parent=NULL;
	bp->links[1].left=NULL;
	bp->links[1].right=NULL;
	//printf("\nRoot created");
	}
	else
	{

	temp=root;
		while(1)
		{
			if(temp>bp && temp->links[1].left==NULL)
			{
			temp->links[1].left=bp;
			bp->links[1].parent=temp;
			break;
			}
			else if(temp>bp && temp->links[1].left!=NULL)
			{
	
			temp=temp->links[1].left;
			}
			else if(temp<bp && temp->links[1].right==NULL)
			{
			temp->links[1].right=bp;
			bp->links[1].parent=temp;
			break;
			}
			else
			{
			temp=temp->links[1].right;
			}
		}
			
	}

}


block_t *split(block_t *found, size_t sb_req)		//function which splits best fit node into two nodes
{

block_t *newptr=(block_t *)((char *)found+sb_req);
newptr->size =found->size - sb_req ;
found->size= sb_req - sizeof(size_t);

newptr->links[0].left = NULL;
newptr->links[0].right = NULL;
newptr->links[0].parent = NULL;
newptr->links[1].left = NULL;
newptr->links[1].right = NULL;
newptr->links[1].parent = NULL;
deletesize(found);
deleteaddress(found);
insert_BST_size(sentinal_node.links[0].left,newptr);
insert_BST_address(sentinal_node.links[1].left,newptr);
void *vp=found;
return vp;
}

void *malloc(size_t sz)		//This function allocates a block of memory of size bytes
{
//printf("\nin malloc function");
size_t sb_req=sz+sizeof(size_t);
//printf("\nroot in malloc=%lu",(uintptr_t)root);

	if(sb_req > sizeof(block_t))
	{
		if(sb_req % 8 != 0)
		{
		sb_req= (sb_req/8)*8+8;
		}
	}
sb_req=sb_req > sizeof(block_t) ? sb_req : sizeof(block_t);
block_t *found,*splitnode;
found=search_bst(sb_req);
	if(found!=NULL)
	{
		int difference=(ssize_t)(found->size + sizeof(size_t)-sb_req);
		if(difference >= 0 && (size_t)difference >= sizeof(block_t))
		{
		splitnode=split(found,sb_req);
		void *vp=(char *)splitnode+ sizeof(size_t);
		
		//printf("\n>>> Allocated %zu old bytes for %zu byte request at %lu from tree.\n", found->size, sz,(uintptr_t)vp);
		return vp;
		}
		else
		{
		deletesize(found);
		deleteaddress(found);
		void *vp=(char *)found+ sizeof(size_t);
		//printf("\n>>> Allocated %zu old bytes for %zu byte request at %lu from tree.\n", found->size, sz,(uintptr_t)vp);
		return vp;
		}
	}

	else
	{
	block_t *new_block = (block_t *)sbrk(sb_req);
	new_block->size=sb_req - sizeof(size_t);
	void *vp=(char *)new_block + sizeof(size_t);
	//printf("\n>>> Allocated %zu new bytes for %zu byte request at %lu from sbrk.\n", new_block->size, sz,(uintptr_t)vp);
	return vp;
	}

}





void free(void *vp)	//This function frees a block of memory that had previously been allocatedfree node
{
//printf("\nin free function");
	if(vp!=NULL)
	{
	block_t *bp = (block_t *) (((char *) vp) - sizeof(size_t));
	//printf("%\ninside freee address %lu",bp);
	insert_BST_size(sentinal_node.links[0].left,bp);
	insert_BST_address(sentinal_node.links[1].left,bp);
	vp=NULL;
	}
return;
}




void *calloc(size_t nmemb, size_t size) // his function allocates memory for an array of nmemb elements of size bytes each
{
//printf("\nin calloc");
void *vp=malloc(nmemb*size);
return vp;
}

void *realloc(void *ptr, size_t size)  //realloc() changes the size of the memory block pointed to by ptr to size bytes
{
//printf("\nin realloc");
block_t *vp;
block_t *found,*splitnode;
	if(ptr==NULL && size !=0)
	{
	return malloc(size);
	}
	else if(ptr!= NULL && size==0)
	{
	free(ptr);
	return NULL;
	}
	else
	{
	vp=(block_t *)((char *)ptr - sizeof(size_t));
		if(vp->size >= size)
		{
		
		vp->size= size;
		//printf("\nreallocated node at address vp=%lu",(uintptr_t)(block_t *)vp+8);
		return ptr;
		

		}
		else
		{
		size_t sb_req=size;
			sb_req=sb_req+sizeof(size_t);	
			if(sb_req > sizeof(block_t))
			{
				if(sb_req % 8 != 0)
				{
				sb_req= (sb_req/8)*8+8;
				}
			}
		sb_req=sb_req > sizeof(block_t) ? sb_req : sizeof(block_t);
		found=search_bst(sb_req);
			if(found!=NULL)
			{
			int difference=(ssize_t)(found->size + sizeof(size_t)-sb_req);
				if(difference >= 0 && (size_t)difference >= sizeof(block_t))
				{
				splitnode=split(found,sb_req);
				void *vp=(char *)splitnode+ sizeof(size_t);
				//printf("\n>>> Allocated %zu old bytes for %zu byte request at %lu from tree.\n", splitnode->size, size,(uintptr_t)splitnode);
				return (char*)vp;
				}
				else
				{
				deletesize(found);
				deleteaddress(found);
				void *vp=(char *)found+ sizeof(size_t);
				//printf("\n>>> Allocated %zu old bytes for %zu byte request at %lu from tree.\n", found->size, size,(uintptr_t)found);
				return (char*)vp;
				}
			}
			else
			{
			block_t *new_block = (block_t *)sbrk(sb_req);
			new_block->size=sb_req - sizeof(size_t);
			void *vp=(char *)new_block + sizeof(size_t);
			//printf("\n>>> Allocated %zu new bytes for %zu byte request at %lu from sbrk.\n", new_block->size, size,(uintptr_t)vp);
			return (char*)vp;
			}
		}
				
	}
}

/*int main()
{
void *vp1, *vp2,*vp3,*vp4,*vp5,*vp6,*vp7,*vp8,*vp9;
        vp1 = malloc(10);
	free(vp1);
	vp1 = malloc(10);
        vp2 = malloc(30);
        free(vp1);
        free(vp2);
        vp2 = malloc(30);
        vp1 = malloc(10);
        free(vp1);
        free(vp2);
        free(malloc(100));
        free(malloc(48));

	vp1 = malloc(500);
	free(vp1);
	vp1 = malloc(100);
        vp2 = malloc(2000);
        free(vp1);
        free(vp2);
        vp2 = malloc(5000);
        vp1 = malloc(10);
        free(vp1);
        free(vp2);
        free(malloc(120));
        free(malloc(130));
	
	vp4=realloc(vp1,50);
	vp5=calloc(3,100);
	free(vp4);
	free(vp5);
	vp6=malloc(600);
	vp6=realloc(vp6,700);
	free(vp6);
	vp4=calloc(2,20);
	free(malloc(100));
        free(malloc(48));
	vp4=realloc(vp4,10);

	vp7=malloc(100);
	vp8=calloc(3,20);
	free(vp7);
	free(vp8);
	vp9=malloc(60);
	vp9=realloc(vp9,700);
	free(vp9);
	vp9=calloc(2,20);
	free(malloc(100));
        free(malloc(48));
	vp9=realloc(vp9,10);
	
}*/
