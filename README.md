
public static void main(String[] args) {

        simpleDLL sdll = simpleDLL.INSTANCE;

        sdll.simpleCall();  // call of void function

        int a = 3;
        int result1 = sdll.giveIntGetInt(a);  // calling function with int parameter&result
        System.out.println("giveIntGetInt("+a+"): " + result1);

        String testStr = "ToBeOrNotToBe";
        Memory mTest = new Memory(testStr.length()+1);  // '+1' remember about extra byte for \0 character!
        mTest.setString(0, testStr);
        String testReturn = mTest.getString(0); // you can see that String got properly stored in Memory object
        System.out.println("String in Memory:"+testReturn);

        Memory intMem = new Memory(4);  // allocating space
        intMem.setInt(0, 666); // setting allocated memory to an integer
        Pointer intPointer = intMem.getPointer(0);

        int int1 = sdll.giveVoidPtrGetInt(Pointer.NULL); // passing null, getting default result
        System.out.println("giveVoidPtrGetInt(null):" + int1); 
        int int2 = sdll.giveVoidPtrGetInt(intMem); // passing int stored in Memory object, getting it back
       //int int2 = sdll.giveVoidPtrGetInt(intPointer);  causes JVM crash, use memory object directly!
        System.out.println("giveVoidPtrGetInt(666):" + int2);

        byte char1 = sdll.giveVoidPtrGetChar(Pointer.NULL);  // passing null, getting default result
        byte char2 = sdll.giveVoidPtrGetChar(mTest);        // passing string stored in Memory object, getting first letter

        System.out.println("giveVoidPtrGetChar(null):" + (char)char1);
        System.out.println("giveVoidPtrGetChar('ToBeOrNotToBe'):" + (char)char2);

    }
}
