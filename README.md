# coonectrpc-errordetail

## validation error

```
% grpcurl \
    -protoset <(buf build -o -) -plaintext \
    -d '{"name": ""}' \
    localhost:8080 greet.v1.GreetService/Greet
```

```
ERROR:
  Code: InvalidArgument
  Message: validation error:
 - name: value is required [required]
  Details:
  1)	{
    	  "@type": "type.googleapis.com/buf.validate.Violations",
    	  "violations": [
    	    {
    	      "fieldPath": "name",
    	      "constraintId": "required",
    	      "message": "value is required"
    	    }
    	  ]
    	}
```

## retry error

code example from [here](https://connectrpc.com/docs/go/errors#error-details)

```
grpcurl \
    -protoset <(buf build -o -) -plaintext \
    -d '{"name": "1"}' \
    localhost:8080 greet.v1.GreetService/Greet
```

```
ERROR:
  Code: Unavailable
  Message: overloaded: back off and retry
  Details:
  1)	{
    	  "@error": "google.rpc.RetryInfo is not recognized; see @value for raw binary message data",
    	  "@type": "type.googleapis.com/google.rpc.RetryInfo",
    	  "@value": "CgIICg=="
    	}
```
