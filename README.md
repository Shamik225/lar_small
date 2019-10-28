# lar_small
To find the largest and smallest element in a binary search tree
#include<stdio.h>
#include<stdlib.h>
struct node
{
  int data;
  struct node * left, * right;
};

struct node * root = NULL;
int small = 0, large = 0;

struct node * create(struct node * root, int num)
{
  if(root == NULL)
  {
    root = (struct node *) malloc(sizeof(struct node));
    root -> data = num;
    root -> left = NULL;
    root -> right = NULL;
    return root;
  }
  else if(root -> data > num)
  {
    root -> left = create(root -> left, num);
    return root;
  }
  else if(root -> data < num)
  {
    root -> right = create(root -> right, num);
    return root;
  }
  else
    return NULL;
}

void pre(struct node * root)
{
  if(root != NULL)
  {
   if(root -> data < small)
    {
      small = root -> data;
    }
   else if(root -> data > large)
    {
      large = root -> data;
    }
   pre(root -> left);
   pre(root -> right);
  }
}

void main()
{
  int ch,n;
  while(ch != 3)
  {
    printf("Enter your choice :\n");
    printf("1.Create\n 2.Pre\n 3.Exit\n");
    scanf("%d",&ch);
    switch(ch)
    {
      case 1: printf("Enter the element:\n");
              scanf("%d",&n);
              root = create(root,n);
              break;

      case 2: small = root -> data;
              printf("Pre order traversal\n");
              pre(root);
              printf("%d %d",large,small);
              break;
       
      case 3:
              break;

         default: printf("Wrong choice\n");
   }
  }
} 
