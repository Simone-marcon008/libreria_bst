#include <iostream>
using namespace std;
struct Node{
    int value;
    Node*left_son;
    Node*right_son;
    Node (){
        left_son=nullptr;
        right_son=nullptr;
    }
    Node (int val){
        value=val;
        left_son=nullptr;
        right_son=nullptr;
    }
};

Node* recursive_search(Node*p,int val){
    if(p==nullptr){
        return p;
    }
    if(p->value==val){
        return p;
    }
    if(p->value<val){
        if(p->right_son==nullptr){
            return nullptr;
        }
        return recursive_search(p->right_son,val);
    }
    if(p->value>val){
        if(p->left_son==nullptr){
            return nullptr;
        }
        return recursive_search(p->left_son,val);
    }
return nullptr;
}
Node* insert(Node* p, int val){
    if(p==nullptr){
        return p=new Node(val);
    }
    if(p->value==val){
        return p;
    }
    if(p->value<val){
         p->right_son=insert(p->right_son,val);
    } else {
        p->left_son=insert(p->left_son,val);
    }
    return p;
}
void preOrder(Node* node){
    if(node==nullptr){
        return;
    }
    cout<<node->value<<" ";
    preOrder(node->left_son);
    preOrder(node->right_son);
}
void inOrder (Node* node){
    if(node==nullptr){
        return;
    }
    inOrder(node->left_son);
    cout<<node->value<<" ";
    inOrder(node->right_son);
}
void postOrder (Node* node){
    if(node==nullptr){
        return;
    }
    postOrder(node->left_son);
    postOrder(node->right_son);
    cout<<node->value<<" ";
}
Node* searchSuccessor(Node* p) {
    Node* ptr=p;
    while ((ptr!=nullptr)&&(ptr->left_son!=nullptr)) {
        ptr=ptr->left_son;
    }
    return ptr;
}
Node* Delete_Node(Node* ptr, int val) {
    if (ptr == nullptr) {
        return nullptr;
    }
    if (val < ptr->value) {
        ptr->left_son = Delete_Node(ptr->left_son, val);
    } else if (val > ptr->value) {
        ptr->right_son = Delete_Node(ptr->right_son, val);
    } else {
        if (ptr->left_son == nullptr && ptr->right_son == nullptr) {
            delete ptr;
            return nullptr;
        } else if (ptr->left_son == nullptr) {
            Node* temp = ptr->right_son;
            delete ptr;
            return temp;
        } else if (ptr->right_son == nullptr) {
            Node* temp = ptr->left_son;
            delete ptr;
            return temp;
        } else {
            Node* ptr_succ = searchSuccessor(ptr->right_son);
            ptr->value = ptr_succ->value;
            ptr->right_son = Delete_Node(ptr->right_son, ptr_succ->value);
        }
    }
    return ptr;
}
