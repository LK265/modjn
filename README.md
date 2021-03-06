modjn
=====

Modbus TCP client/server implementation in Java with Netty 4.x

## Currently implemented modbus functions

*    READ COILS | 0x01
*    READ DISCRETE INPUTS | 0x02
*    READ HOLDING REGISTERS | 0x03
*    READ INPUT REGISTERS | 0x04
*    WRITE SINGLE COIL | 0x05
*    WRITE SINGLE REGISTER | 0x06
*    WRITE MULTIPLE COILS | 0x0F
*    WRITE MULTIPLE REGISTERS | 0x10

## Usage

### Server

implement ModbusRequestHandler for server business logic, example [here...](https://github.com/klymenek/modjn/blob/master/src/main/java/de/gandev/modjn/example/ModbusRequestHandlerExample.java)


    ModbusServer modbusServer = new ModbusServer(502);

    try {
        modbusServer.setup(new ModbusRequestHandler());
    } catch(ConnectionException ex) {
        System.out.println(ex.getLocalizedMessage());
    }

    modbusServer.close();

### Client

switch to async requests by passing an instance of ModbusResponseHandler to the setup function and handle responses by yourself


    ModbusClient modbusClient = new ModbusClient("localhost"; 502);

    try {
        modbusClient.setup();

        ReadCoilsResponse readCoils = modbusClient.readCoils(12321, 10);

        //modbusClient.[other functions] ...

        System.out.println(readCoils);
    } catch (NoResponseException | ErrorResponseException | ConnectionException ex) {
        System.out.println(ex.getLocalizedMessage());
    }

    modbusClient.close();
