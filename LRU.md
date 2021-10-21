 /**
     * LRU缓存淘汰算法-最近最少使用
     * 增加和删除 快，采用链表实现
     * 查询和修改 快，采用数组实现
     */
     
   static final class LRU{

        private Map<Integer,Node<Integer,Integer>> table=new HashMap<>(16);

        private int cacheSize;

        private ListNode<Integer,Integer> listNode;

        LRU(int cacheSize){
            this.cacheSize = cacheSize;
            listNode=new ListNode<>();
        }

        private int get(int key){
            if(!table.containsKey(key)){
                return -1;
            }
            Node<Integer,Integer> node=table.get(key);
            //从链表的位置删除节点并添加到队头
            listNode.removeNode(node);
            listNode.addFirst(node);
            return node.value;
        }

        private void put(int key,int value){
            if(table.containsKey(key)){
                Node<Integer,Integer> node=table.get(key);
                node.value=value;
                table.put(key,node);
                listNode.removeNode(node);
                listNode.addFirst(node);
            }else{
                //如果容量满了,删除map和链表中的节点
                if(table.size()==cacheSize){
                    Node<Integer,Integer> last=listNode.getTail();
                    table.remove(last.key);
                    listNode.removeNode(last);
                }
                Node<Integer,Integer> newNode=new Node<>(key,value);
                listNode.addFirst(newNode);
                table.put(key,newNode);
            }
        }

        static class Node<K,V>{
            private K key;
            private V value;
            private Node<K,V> prev;
            private Node<K, V> next;

            Node(K key,V value){
                this.key=key;
                this.value=value;
                this.prev=this.next=null;
            }
             Node(){
                this.prev=null;
                this.next=null;
            }
        }

        static class ListNode<K,V>{
            private Node<K,V> head;
            private Node<K,V> tail;

             ListNode(){
                head=new Node<>();
                tail=new Node<>();
                head.next=tail;
                tail.prev=head;
            }

            ///将元素添加到头节点
            private void addFirst(Node<K,V> node){
                node.prev=head;
                node.next=head.next;
                head.next.prev=node;
                head.next=node;
            }
            //删除节点
            private void removeNode(Node<K,V> node){
                node.prev.next=node.next;
                node.next.prev=node.prev;
                node.prev=null;
                node.next=null;
            }

            //获取最后一个节点
            private Node<K,V> getTail(){
                return tail.prev;
            }



        }
    }
