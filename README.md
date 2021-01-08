# NAME

Confluent::SchemaRegistry - A simple client for interacting with **Confluent Schema Registry**.

# SYNOPSIS

    use Confluent::SchemaRegistry;

    my $sr = Confluent::SchemaRegistry->new( { host => 'https://my-schema-registry.org' } );

# DESCRIPTION

`Confluent::SchemaRegistry` provides a simple way to interact with **Confluent Schema Registry**
([https://docs.confluent.io/current/schema-registry/docs/index.html](https://docs.confluent.io/current/schema-registry/docs/index.html)) enabling writing into
**Apache Kafka** ([https://kafka.apache.org/](https://kafka.apache.org/)) according to _Apache Avro_ schema specification
([https://avro.apache.org/](https://avro.apache.org/)).

## HEAD UP

- Confluent Schema Registry documentation

    Full RESTful API documentation of **Schema Registry** is available here: 
    [https://docs.confluent.io/current/schema-registry/docs/api.html?\_ga=2.234767710.1188695207.1526911788-1213051144.1524553242#](https://docs.confluent.io/current/schema-registry/docs/api.html?_ga=2.234767710.1188695207.1526911788-1213051144.1524553242#)

- Avro package

    **Avro** package is a dependency of _Confluent::SchemaRegistry_ but is not available in CPAN index.
    Perhaps you may find and download it directly from GitHub repository at [https://github.com/apache/avro/tree/master/lang/perl](https://github.com/apache/avro/tree/master/lang/perl).
    Please, refer its documentation for installation.

# INSTALL

Installation of `Kafka::Consumer::Avro` is a canonical:

    perl Makefile.PL
    make
    make test
    make install

## TEST NOTES

Tests expect that in the target host is available Schema Registry listening on `http://localhost:8081`, otherwise most of the test are skipped.

You can alternatively set a different URL by exporting `CONFLUENT_SCHEMA_REGISTY_URL` environment variable.

# USAGE

## Constructor

### new( \[%config\] )

Construct a new `Confluent::SchemaRegistry`. Takes an optional hash that provides
configuration flags for the [REST::Client](https://metacpan.org/pod/REST%3A%3AClient) internal object.

The config flags, according to `REST::Client::new` specs, are:

- host

    The host at which _Schema Registry_ is listening.

    The default is [http://localhost:8081](http://localhost:8081)

- timeout

    A timeout in seconds for requests made with the client.  After the timeout the
    client will return a 500.

    The default is 5 minutes.

- cert

    The path to a X509 certificate file to be used for client authentication.

    The default is to not use a certificate/key pair.

- key

    The path to a X509 key file to be used for client authentication.

    The default is to not use a certificate/key pair.

- ca

    The path to a certificate authority file to be used to verify host
    certificates.

    The default is to not use a certificates authority.

- pkcs12

    The path to a PKCS12 certificate to be used for client authentication.

- pkcs12password

    The password for the PKCS12 certificate specified with 'pkcs12'.

- follow

    Boolean that determins whether REST::Client attempts to automatically follow
    redirects/authentication.

    The default is false.

- useragent

    An [LWP::UserAgent](https://metacpan.org/pod/LWP%3A%3AUserAgent) object, ready to make http requests.

    REST::Client will provide a default for you if you do not set this.

## METHODS

`Confluent::SchemRegistry` exposes the following methods.

### get\_response\_content()

Returns the body (content) of the last method call to Schema Registry.

### get\_error()

Returns the error structure of the last method call to Schema Registry.

### add\_schema( %params )

Registers a new schema version under a subject.

Returns the generated id for the new schema or `undef`.

Params keys are:

- SUBJECT ($scalar)

    the name of the Kafka topic

- TYPE ($scalar)

    the type of schema ("key" or "value")

- SCHEMA ($hashref or $json)

    the schema to add

# TODO

...

# AUTHOR

Alvaro Livraghi, <alvarol@cpan.org>

# CONTRIBUTE

[https://github.com/alivraghi/Confluent-SchemaRegistry](https://github.com/alivraghi/Confluent-SchemaRegistry)

# BUGS

Please use GitHub project link above to report problems or contact authors.

# COPYRIGHT AND LICENSE

Copyright 2018 by Alvaro Livraghi

This program is free software; you can redistribute it and/or modify it under the same terms as Perl itself.
