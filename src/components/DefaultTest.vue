<template>
  <div id="default-container">
    <div id="log">
        <pre>
          <p>{{log}}</p>
        </pre>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { useStorageSQLite } from 'vue-data-storage-sqlite-hook/dist';
import { useState } from '@/composables/state';

export default defineComponent({
  name: 'DefaultTest',
  async setup() {
    const [log, setLog] = useState("");
    const { openStore, getItem, setItem, getAllKeys, getAllValues,
            getAllKeysValues, isKey, removeItem,
            clear} = useStorageSQLite();
    setLog(log.value.concat("**** Starting Test Default Store ****\n")); 
    // open store
    const resOpen: boolean = await openStore({});
    if( !resOpen ) {
      setLog(log.value.concat("openStore failed \n"));
      return { log };
    } else {
      setLog(log.value.concat("openStore was successful \n"));
    }
    // clear the store 
    const rClear: boolean = await clear();
    if( !rClear ) {
      setLog(log.value.concat("clear failed \n"));
      return { log };
    } else {
      setLog(log.value.concat("clear was successful \n"));
    }
    // store a string 
    await setItem("session","Session Opened");
    const session = await getItem('session');
    if(session != "Session Opened") {
      setLog(log.value.concat("setItem/getItem session failed \n"));
      return { log };
    } else {
      setLog(log.value.concat("setItem/getItem session was successful \n"));
    }
    // store a JSON Object in the default store
    const data = {'a':20,'b':'Hello World','c':{'c1':40,'c2':'cool'}};
    await setItem("testJson",JSON.stringify(data));
    const testJson = await getItem("testJson");
    if( testJson != JSON.stringify(data) ) {
      setLog(log.value.concat("setItem/getItem testJson failed \n"));
      return { log };
    } else {
      setLog(log.value
            .concat("setItem/getItem testJson was successful \n"));
    }
    // store a number in the default store
    const data1 = 243.567;
    await setItem("testNumber",data1.toString());
    // read number from the store
    const testNumber = Number(await getItem("testNumber"));
    if( testNumber != data1 ) {
      setLog(log.value.concat("setItem/getItem testNumber failed \n"));
      return { log };
    } else {
      setLog(log.value
          .concat("setItem/getItem testNumber was successful \n"));
    }
    // isKey tests
    const iskey: boolean = await isKey('testNumber');
    if( !iskey ) {
      setLog(log.value.concat("isKey testNumber failed \n"));
      return { log };
    } else {
      setLog(log.value.concat("isKey testNumber was successful \n"));
    }
    const iskey1: boolean = await isKey('foo');
    if( iskey1 ) {
      setLog(log.value.concat("isKey foo failed \n"));
      return { log };
    } else {
      setLog(log.value.concat("isKey foo was successful \n"));
    }
    // Get All Keys
    const keys: string[] = await getAllKeys();
    if(keys.length != 3) {
      setLog(log.value.concat("getAllKeys failed \n"));
      return { log };
    } else {
      for(let i = 0; i< keys.length;i++) {
        setLog(log.value.concat(' key[' + i + "] = " + keys[i] + "\n"));
      }
      setLog(log.value.concat("getAllKeys was successful \n"));
    }
    // Get All Values
    const values: string[] = await getAllValues();
    if(values.length != 3) {
      setLog(log.value.concat("getAllValues failed \n"));
      return { log };
    } else {
      for(let i = 0; i< values.length;i++) {
        setLog(log.value.concat(' key[' + i + "] = " + values[i] + "\n"));
      }
      setLog(log.value.concat("getAllValues was successful \n"));
    }
    // Get All KeysValues
    const keysvalues: any[] = await getAllKeysValues();
    if(keysvalues.length != 3) {
      setLog(log.value.concat("getAllKeysValues failed \n"));
      return { log };
    } else {
      setLog(log.value.concat("getAllKeysValues was successful \n"));
    }
    // Remove a key 
    const res: boolean = await removeItem('testJson')
    if( !res ) {
      setLog(log.value.concat("removeItem failed \n"));
      return { log };
    } else {
      setLog(log.value.concat("removeItem was successful \n"));
    }
    // Get All Keys
    const keys1: string[] = await getAllKeys();
    if(keys1.length != 2) {
      setLog(log.value.concat("getAllKeys after removeItem failed \n"));
      return { log };
    } else {
      for(let i = 0; i< keys1.length;i++) {
        setLog(log.value.concat(' key[' + i + "] = " + keys1[i] + "\n"));
      }
      setLog(log.value
            .concat("getAllKeys after removeItem was successful \n"));
    }
    setLog(log.value
          .concat("\n**** Test Default Store was successful ****\n")); 
    return { log };
  }

});
</script>
